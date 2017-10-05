---
title: "SQL Server kullanılabilirlik gruplarını - Azure sanal makineleri - genel bakış | Microsoft Docs"
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
ms.openlocfilehash: 2cbb9ff3b2d13996b1b8dc64aa833807c264c877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="54f47-103">SQL Server Always On kullanılabilirlik grupları'Azure sanal makinelerde Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="54f47-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="54f47-104">Bu makalede, SQL Server kullanılabilirlik gruplarını Azure sanal makineler üzerinde tanıtılır.</span><span class="sxs-lookup"><span data-stu-id="54f47-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="54f47-105">Always On kullanılabilirlik grupları Azure sanal makineler üzerinde Always On kullanılabilirlik grupları şirket içi benzerdir.</span><span class="sxs-lookup"><span data-stu-id="54f47-105">Always On availability groups on Azure Virtual Machines are similar to Always On availability groups on premises.</span></span> <span data-ttu-id="54f47-106">Daha fazla bilgi için bkz: [Always On kullanılabilirlik grupları (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f47-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="54f47-107">Diyagram tam SQL Server kullanılabilirlik grubu Azure Virtual Machines'de parçalarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="54f47-107">The diagram illustrates the parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="54f47-109">En önemli fark, Azure sanal makineleri bir kullanılabilirlik grubu için Azure sanal makinelerini gerekmesidir bir [yük dengeleyici](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54f47-109">The key difference for an Availability Group in Azure Virtual Machines is that the Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="54f47-110">Yük Dengeleyici için kullanılabilirlik grubu dinleyici IP adreslerini tutar.</span><span class="sxs-lookup"><span data-stu-id="54f47-110">The load balancer holds the IP addresses for the availability group listener.</span></span> <span data-ttu-id="54f47-111">Birden çok kullanılabilirlik grubu varsa, her grubun bir dinleyici gerektirir.</span><span class="sxs-lookup"><span data-stu-id="54f47-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="54f47-112">Bir yük dengeleyici birden çok dinleyici destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="54f47-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="54f47-113">Azure Virtual Machines'de SQL Server kullanılabilirlik aroup oluşturmak hazır olduğunuzda bu öğreticileri bakın.</span><span class="sxs-lookup"><span data-stu-id="54f47-113">When you are ready to build a SQL Server availability aroup on Azure Virtual Machines, refer to these tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="54f47-114">Otomatik olarak bir şablondan bir kullanılabilirlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="54f47-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="54f47-115">Always On kullanılabilirlik grubu Azure VM'de otomatik olarak - Resource Manager yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="54f47-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="54f47-116">Azure portalında bir kullanılabilirlik grubu el ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="54f47-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="54f47-117">Sanal makineleri kendiniz olmadan şablon oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54f47-117">You can also create the virtual machines yourself without the template.</span></span> <span data-ttu-id="54f47-118">İlk olarak, önkoşulları tamamlamanız sonra kullanılabilirlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54f47-118">First, complete the prerequisites, then create the availability group.</span></span> <span data-ttu-id="54f47-119">Aşağıdaki konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="54f47-119">See the following topics:</span></span> 

- [<span data-ttu-id="54f47-120">Azure Virtual Machines'de SQL Server Always On kullanılabilirlik grupları için önkoşulları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="54f47-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="54f47-121">Her zaman üzerinde kullanılabilirlik kullanılabilirlik ve olağanüstü durum kurtarma artırmak için grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="54f47-121">Create Always On Availability Group to improve availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="54f47-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54f47-122">Next steps</span></span>

<span data-ttu-id="54f47-123">[Bir SQL Server kullanılabilirlik grubu de farklı bölgelerdeki Azure sanal makinelerde her zaman yapılandırmasına](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="54f47-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
