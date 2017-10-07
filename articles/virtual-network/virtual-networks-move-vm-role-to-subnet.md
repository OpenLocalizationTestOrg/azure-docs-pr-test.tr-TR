---
title: "aaaMove bir VM'ye (Klasik) veya Bulut Hizmetleri rol örneği tooa farklı alt ağ - Azure PowerShell | Microsoft Docs"
description: "Bilgi nasıl toomove VM'ler (Klasik) ve bulut Hizmetleri rolü örnekleri PowerShell kullanarak tooa farklı alt ağ."
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
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a><span data-ttu-id="67db1-103">Bir VM'yi (Klasik) veya PowerShell kullanarak bulut Hizmetleri rol örneği tooa farklı alt ağ taşıma</span><span class="sxs-lookup"><span data-stu-id="67db1-103">Move a VM (Classic) or Cloud Services role instance tooa different subnet using PowerShell</span></span>
<span data-ttu-id="67db1-104">PowerShell toomove, VM'lerin (Klasik) bir alt ağ tooanother hello kullanabileceğiniz aynı sanal ağ (VNet).</span><span class="sxs-lookup"><span data-stu-id="67db1-104">You can use PowerShell toomove your VMs (Classic) from one subnet tooanother in hello same virtual network (VNet).</span></span> <span data-ttu-id="67db1-105">Rol örnekleri hello CSCFG dosyası düzenleme yerine PowerShell kullanarak taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="67db1-105">Role instances can be moved by editing hello CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="67db1-106">Bu makalede toomove VM'ler yalnızca hello Klasik dağıtım modeli nasıl dağıtılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="67db1-106">This article explains how toomove VMs deployed through hello classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="67db1-107">Neden VM'ler tooanother alt taşıma?</span><span class="sxs-lookup"><span data-stu-id="67db1-107">Why move VMs tooanother subnet?</span></span> <span data-ttu-id="67db1-108">Alt ağ geçiş olduğunda yararlı hello eski alt ağı çok küçük ve son genişletilemiyor o alt ağdaki sanal makineleri çalıştıran tooexisting.</span><span class="sxs-lookup"><span data-stu-id="67db1-108">Subnet migration is useful when hello older subnet is too small and cannot be expanded due tooexisting running VMs in that subnet.</span></span> <span data-ttu-id="67db1-109">Bu durumda, yeni, büyük bir alt ağ oluşturmak ve hello VM'ler toohello yeni alt ağ geçirmek ardından geçiş tamamlandıktan sonra eski boş alt hello silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67db1-109">In that case, you can create a new, larger subnet and migrate hello VMs toohello new subnet, then after migration is complete, you can delete hello old empty subnet.</span></span>

## <a name="how-toomove-a-vm-tooanother-subnet"></a><span data-ttu-id="67db1-110">Nasıl toomove VM tooanother alt ağı</span><span class="sxs-lookup"><span data-stu-id="67db1-110">How toomove a VM tooanother subnet</span></span>
<span data-ttu-id="67db1-111">bir VM toomove Merhaba örneği aşağıda şablon olarak kullanıp hello kümesi AzureSubnet PowerShell cmdlet'ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="67db1-111">toomove a VM, run hello Set-AzureSubnet PowerShell cmdlet, using hello example below as a template.</span></span> <span data-ttu-id="67db1-112">Merhaba aşağıdaki örnekte, biz TestVM mevcut alt ağ üzerinden, taşıdığınız tooSubnet-2.</span><span class="sxs-lookup"><span data-stu-id="67db1-112">In hello example below, we are moving TestVM from its present subnet, tooSubnet-2.</span></span> <span data-ttu-id="67db1-113">Ortamınızı emin tooedit hello örnek tooreflect olabilir.</span><span class="sxs-lookup"><span data-stu-id="67db1-113">Be sure tooedit hello example tooreflect your environment.</span></span> <span data-ttu-id="67db1-114">Her bir yordam bir parçası olarak hello güncelleştirme-AzureVM cmdlet'ini çalıştırdığınızda, hello güncelleştirme işleminin bir parçası, VM başlayacaktır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="67db1-114">Note that whenever you run hello Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of hello update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="67db1-115">VM için statik iç özel IP belirtilmişse, bu ayarı hello VM tooa yeni alt taşımadan önce tooclear gerekir.</span><span class="sxs-lookup"><span data-stu-id="67db1-115">If you specified a static internal private IP for your VM, you'll have tooclear that setting before you can move hello VM tooa new subnet.</span></span> <span data-ttu-id="67db1-116">Bu durumda, hello aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="67db1-116">In that case, use hello following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a><span data-ttu-id="67db1-117">bir rol örneği tooanother alt toomove</span><span class="sxs-lookup"><span data-stu-id="67db1-117">toomove a role instance tooanother subnet</span></span>
<span data-ttu-id="67db1-118">bir rol örneği toomove hello CSCFG dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="67db1-118">toomove a role instance, edit hello CSCFG file.</span></span> <span data-ttu-id="67db1-119">Merhaba aşağıdaki örnekte, biz "Role0" sanal ağında taşıyor *vnetname adlı* mevcut alt ağdan çok*alt ağ-2*.</span><span class="sxs-lookup"><span data-stu-id="67db1-119">In hello example below, we are moving "Role0" in virtual network *VNETName* from its present subnet too*Subnet-2*.</span></span> <span data-ttu-id="67db1-120">Merhaba rol örneği zaten dağıtılmış olduğundan, hello alt ağ adı yalnızca değiştireceğiz = alt ağ-2.</span><span class="sxs-lookup"><span data-stu-id="67db1-120">Because hello role instance was already deployed, you'll just change hello Subnet name = Subnet-2.</span></span> <span data-ttu-id="67db1-121">Ortamınızı emin tooedit hello örnek tooreflect olabilir.</span><span class="sxs-lookup"><span data-stu-id="67db1-121">Be sure tooedit hello example tooreflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
