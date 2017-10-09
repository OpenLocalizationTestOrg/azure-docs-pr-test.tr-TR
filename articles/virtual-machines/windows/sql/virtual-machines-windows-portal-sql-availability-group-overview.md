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
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a>SQL Server Always On kullanılabilirlik grupları'Azure sanal makinelerde Tanıtımı #

Bu makalede, SQL Server kullanılabilirlik gruplarını Azure sanal makineler üzerinde tanıtılır. 

Always On kullanılabilirlik grupları Azure sanal makineler üzerinde benzer tooAlways şirket içi kullanılabilirlik grupları ' dir. Daha fazla bilgi için bkz: [Always On kullanılabilirlik grupları (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx). 

Merhaba diyagram tam SQL Server kullanılabilirlik grubu Azure Virtual Machines'de hello parçalarını gösterir.

![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

Merhaba anahtar fark bir kullanılabilirlik grubu Azure Virtual Machines'de Azure sanal makinelerde hello için gerektiren bir [yük dengeleyici](../../../load-balancer/load-balancer-overview.md). Merhaba yük dengeleyici hello IP adreslerini hello kullanılabilirlik grubu dinleyicisinin tutar. Birden çok kullanılabilirlik grubu varsa, her grubun bir dinleyici gerektirir. Bir yük dengeleyici birden çok dinleyici destekleyebilir.

Hazır toobuild bir SQL Server kullanılabilirlik aroup Azure sanal makineler üzerinde olduğunda toothese öğreticileri bakın.

## <a name="automatically-create-an-availability-group-from-a-template"></a>Otomatik olarak bir şablondan bir kullanılabilirlik grubu oluşturun

[Always On kullanılabilirlik grubu Azure VM'de otomatik olarak - Resource Manager yapılandırın.](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a>Azure portalında bir kullanılabilirlik grubu el ile oluşturma

Merhaba sanal makineleri kendiniz olmadan hello şablon oluşturabilirsiniz. Öncelikle hello önkoşulları tamamlamanız ardından hello kullanılabilirlik grubu oluşturun. Aşağıdaki konularda hello bakın: 

- [Azure Virtual Machines'de SQL Server Always On kullanılabilirlik grupları için önkoşulları yapılandırma](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [Her zaman üzerinde kullanılabilirlik grubu oluşturma tooimprove kullanılabilirlik ve olağanüstü durum kurtarma](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a>Sonraki adımlar

[Bir SQL Server kullanılabilirlik grubu de farklı bölgelerdeki Azure sanal makinelerde her zaman yapılandırmasına](virtual-machines-windows-portal-sql-availability-group-dr.md).
