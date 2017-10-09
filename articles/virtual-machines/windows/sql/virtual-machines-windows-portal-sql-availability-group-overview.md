---
title: "aaaSQL Server kullanılabilirlik gruplarını - Azure sanal makineleri - genel bakış | Microsoft Docs"
description: "Bu makalede, Azure sanal makinelerde SQL Server kullanılabilirlik gruplarını tanıtılır."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="f7f47-103">SQL Server Always On kullanılabilirlik grupları'Azure sanal makinelerde Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="f7f47-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="f7f47-104">Bu makalede, SQL Server kullanılabilirlik gruplarını Azure sanal makineler üzerinde tanıtılır.</span><span class="sxs-lookup"><span data-stu-id="f7f47-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="f7f47-105">Always On kullanılabilirlik grupları Azure sanal makineler üzerinde benzer tooAlways şirket içi kullanılabilirlik grupları ' dir.</span><span class="sxs-lookup"><span data-stu-id="f7f47-105">Always On availability groups on Azure Virtual Machines are similar tooAlways On availability groups on premises.</span></span> <span data-ttu-id="f7f47-106">Daha fazla bilgi için bkz: [Always On kullanılabilirlik grupları (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="f7f47-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="f7f47-107">Merhaba diyagram tam SQL Server kullanılabilirlik grubu Azure Virtual Machines'de hello parçalarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f7f47-107">hello diagram illustrates hello parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="f7f47-109">Merhaba anahtar fark bir kullanılabilirlik grubu Azure Virtual Machines'de Azure sanal makinelerde hello için gerektiren bir [yük dengeleyici](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7f47-109">hello key difference for an Availability Group in Azure Virtual Machines is that hello Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="f7f47-110">Merhaba yük dengeleyici hello IP adreslerini hello kullanılabilirlik grubu dinleyicisinin tutar.</span><span class="sxs-lookup"><span data-stu-id="f7f47-110">hello load balancer holds hello IP addresses for hello availability group listener.</span></span> <span data-ttu-id="f7f47-111">Birden çok kullanılabilirlik grubu varsa, her grubun bir dinleyici gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f7f47-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="f7f47-112">Bir yük dengeleyici birden çok dinleyici destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="f7f47-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="f7f47-113">Hazır toobuild bir SQL Server kullanılabilirlik aroup Azure sanal makineler üzerinde olduğunda toothese öğreticileri bakın.</span><span class="sxs-lookup"><span data-stu-id="f7f47-113">When you are ready toobuild a SQL Server availability aroup on Azure Virtual Machines, refer toothese tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="f7f47-114">Otomatik olarak bir şablondan bir kullanılabilirlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="f7f47-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="f7f47-115">Always On kullanılabilirlik grubu Azure VM'de otomatik olarak - Resource Manager yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f7f47-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="f7f47-116">Azure portalında bir kullanılabilirlik grubu el ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7f47-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="f7f47-117">Merhaba sanal makineleri kendiniz olmadan hello şablon oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7f47-117">You can also create hello virtual machines yourself without hello template.</span></span> <span data-ttu-id="f7f47-118">Öncelikle hello önkoşulları tamamlamanız ardından hello kullanılabilirlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f7f47-118">First, complete hello prerequisites, then create hello availability group.</span></span> <span data-ttu-id="f7f47-119">Aşağıdaki konularda hello bakın:</span><span class="sxs-lookup"><span data-stu-id="f7f47-119">See hello following topics:</span></span> 

- [<span data-ttu-id="f7f47-120">Azure Virtual Machines'de SQL Server Always On kullanılabilirlik grupları için önkoşulları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f7f47-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="f7f47-121">Her zaman üzerinde kullanılabilirlik grubu oluşturma tooimprove kullanılabilirlik ve olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="f7f47-121">Create Always On Availability Group tooimprove availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="f7f47-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f7f47-122">Next steps</span></span>

<span data-ttu-id="f7f47-123">[Bir SQL Server kullanılabilirlik grubu de farklı bölgelerdeki Azure sanal makinelerde her zaman yapılandırmasına](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="f7f47-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
