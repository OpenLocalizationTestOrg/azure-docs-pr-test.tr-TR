---
title: "MySQL bir OpenSUSE VM olanağına yükle | Microsoft Docs"
description: "Azure'da OpenSUSE Linux VMirtual makine MySQL yüklemek öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 01b798a25575b66f89057315ce80d6cc0cde53b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="f30d7-103">Azure'da OpenSUSE Linux çalıştıran bir sanal makineye MySQL yükleme</span><span class="sxs-lookup"><span data-stu-id="f30d7-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="f30d7-104">[MySQL] [ MySQL] popüler, açık kaynaklı bir SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="f30d7-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="f30d7-105">Bu öğretici OpenSUSE Linux çalıştıran bir sanal makine oluşturun ve MySQL yükleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f30d7-105">This tutorial shows you how to create a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f30d7-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f30d7-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f30d7-107">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="f30d7-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="f30d7-108">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="f30d7-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="f30d7-109">OpenSUSE Linux çalıştıran bir sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="f30d7-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-the-virtual-machine"></a><span data-ttu-id="f30d7-110">Yükleme ve sanal makinede MySQL çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f30d7-110">Install and run MySQL on the virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="f30d7-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f30d7-111">Next steps</span></span>
<span data-ttu-id="f30d7-112">MySQL hakkında daha fazla ayrıntı için bkz: [MySQL belgeleri][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="f30d7-112">For details about MySQL, see the [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

