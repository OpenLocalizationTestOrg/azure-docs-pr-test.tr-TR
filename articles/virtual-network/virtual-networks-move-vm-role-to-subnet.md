---
title: "Bir VM'yi (Klasik) veya Bulut Hizmetleri rol örneği farklı bir alt - Azure PowerShell taşıma | Microsoft Docs"
description: "PowerShell kullanarak farklı bir alt ağa VM'ler (Klasik) ve bulut Hizmetleri rol örnekleri taşıma öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b094f8338394ef2e84cad3070936d715411326a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-to-a-different-subnet-using-powershell"></a><span data-ttu-id="e871e-103">PowerShell kullanarak farklı bir alt ağa bir VM (Klasik) veya Bulut Hizmetleri rol örneğini taşıma</span><span class="sxs-lookup"><span data-stu-id="e871e-103">Move a VM (Classic) or Cloud Services role instance to a different subnet using PowerShell</span></span>
<span data-ttu-id="e871e-104">Vm'leriniz (Klasik) bir alt ağdan başka bir programda aynı sanal ağ (VNet) taşımak için PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="e871e-104">You can use PowerShell to move your VMs (Classic) from one subnet to another in the same virtual network (VNet).</span></span> <span data-ttu-id="e871e-105">Rol örnekleri CSCFG dosyası düzenleme yerine PowerShell kullanarak taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="e871e-105">Role instances can be moved by editing the CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="e871e-106">Bu makalede VM'ler yalnızca klasik dağıtım modeli aracılığıyla dağıtılan taşıma konusunda açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e871e-106">This article explains how to move VMs deployed through the classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="e871e-107">Neden sanal makineleri başka bir alt ağa taşıyın?</span><span class="sxs-lookup"><span data-stu-id="e871e-107">Why move VMs to another subnet?</span></span> <span data-ttu-id="e871e-108">Alt ağ geçiş eski alt ağı çok küçük ve bu alt ağdaki var olan çalışan sanal makinelerini nedeniyle genişletilemiyor faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="e871e-108">Subnet migration is useful when the older subnet is too small and cannot be expanded due to existing running VMs in that subnet.</span></span> <span data-ttu-id="e871e-109">Bu durumda, yeni, büyük bir alt ağ oluşturmak ve yeni bir alt ağ için sanal makineleri geçirmek ardından geçiş tamamlandıktan sonra eski boş alt silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e871e-109">In that case, you can create a new, larger subnet and migrate the VMs to the new subnet, then after migration is complete, you can delete the old empty subnet.</span></span>

## <a name="how-to-move-a-vm-to-another-subnet"></a><span data-ttu-id="e871e-110">Başka bir alt ağ için bir VM taşıma</span><span class="sxs-lookup"><span data-stu-id="e871e-110">How to move a VM to another subnet</span></span>
<span data-ttu-id="e871e-111">Bir VM taşımak için aşağıdaki örnekte bir şablon olarak kullanıp kümesi AzureSubnet PowerShell cmdlet'ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e871e-111">To move a VM, run the Set-AzureSubnet PowerShell cmdlet, using the example below as a template.</span></span> <span data-ttu-id="e871e-112">Aşağıdaki örnekte, biz TestVM mevcut kendi alt ağdan alt ağ-2'ye taşıyor.</span><span class="sxs-lookup"><span data-stu-id="e871e-112">In the example below, we are moving TestVM from its present subnet, to Subnet-2.</span></span> <span data-ttu-id="e871e-113">Ortamınızı yansıtmak üzere örnek düzenlemek emin olun.</span><span class="sxs-lookup"><span data-stu-id="e871e-113">Be sure to edit the example to reflect your environment.</span></span> <span data-ttu-id="e871e-114">Her bir yordam bir parçası olarak güncelleştirme-AzureVM cmdlet'ini çalıştırdığınızda, güncelleştirme işleminin bir parçası olarak, VM başlayacaktır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e871e-114">Note that whenever you run the Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of the update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="e871e-115">VM için statik iç özel IP belirtilmişse, yeni bir alt ağ için VM taşımadan önce bu ayarı temizlemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="e871e-115">If you specified a static internal private IP for your VM, you'll have to clear that setting before you can move the VM to a new subnet.</span></span> <span data-ttu-id="e871e-116">Bu durumda, aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="e871e-116">In that case, use the following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="to-move-a-role-instance-to-another-subnet"></a><span data-ttu-id="e871e-117">Başka bir alt ağ için bir rol örneği taşımak için</span><span class="sxs-lookup"><span data-stu-id="e871e-117">To move a role instance to another subnet</span></span>
<span data-ttu-id="e871e-118">Rol örneği taşımak için CSCFG dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="e871e-118">To move a role instance, edit the CSCFG file.</span></span> <span data-ttu-id="e871e-119">Aşağıdaki örnekte, biz "Role0" sanal ağında taşıyor *vnetname adlı* mevcut kendi alt ağdan *alt ağ-2*.</span><span class="sxs-lookup"><span data-stu-id="e871e-119">In the example below, we are moving "Role0" in virtual network *VNETName* from its present subnet to *Subnet-2*.</span></span> <span data-ttu-id="e871e-120">Rol örneği zaten dağıtılmış olduğundan, alt ağ adı yalnızca değiştireceğiz = alt ağ-2.</span><span class="sxs-lookup"><span data-stu-id="e871e-120">Because the role instance was already deployed, you'll just change the Subnet name = Subnet-2.</span></span> <span data-ttu-id="e871e-121">Ortamınızı yansıtmak üzere örnek düzenlemek emin olun.</span><span class="sxs-lookup"><span data-stu-id="e871e-121">Be sure to edit the example to reflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
