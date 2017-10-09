---
title: aaaInstall OpenSUSE VM'de MySQL | Microsoft Docs
description: "Tooinstall MySQL, azure'da OpenSUSE Linux VMirtual makinede öğrenin."
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
ms.openlocfilehash: 8f96d29f29cb9c466dd7fdaf92b378783fdaacd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="52f58-103">Azure'da OpenSUSE Linux çalıştıran bir sanal makineye MySQL yükleme</span><span class="sxs-lookup"><span data-stu-id="52f58-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="52f58-104">[MySQL] [ MySQL] popüler, açık kaynaklı bir SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="52f58-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="52f58-105">Bu öğreticide gösterilmiştir nasıl toocreate OpenSUSE Linux çalıştıran bir sanal makine kurun MySQL.</span><span class="sxs-lookup"><span data-stu-id="52f58-105">This tutorial shows you how toocreate a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="52f58-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="52f58-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="52f58-107">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="52f58-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="52f58-108">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="52f58-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="52f58-109">OpenSUSE Linux çalıştıran bir sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="52f58-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a><span data-ttu-id="52f58-110">Yükleyin ve MySQL hello sanal makinede çalıştırın</span><span class="sxs-lookup"><span data-stu-id="52f58-110">Install and run MySQL on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="52f58-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="52f58-111">Next steps</span></span>
<span data-ttu-id="52f58-112">Merhaba MySQL hakkında daha fazla bilgi için bkz [MySQL belgeleri][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="52f58-112">For details about MySQL, see hello [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

