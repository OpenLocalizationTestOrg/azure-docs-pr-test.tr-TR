---
title: "aaaAvailability Klasik Linux VM'ler için ayarlar | Microsoft Docs"
description: "Kullanılabilirlik kümesi hello Klasik dağıtım modelinde hello Azure portalı ve Azure PowerShell kullanarak yeni veya var olan Linux sanal makine için yapılandırın."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b8624315-beca-4ec7-8441-2e98b166b548
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: cynthn
ms.openlocfilehash: 8d8d041e3540e42a1921f5665469a2fdcaa30a29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-availability-set-for-linux-virtual-machines-in-hello-classic-deployment-model"></a><span data-ttu-id="0a92c-103">Nasıl tooconfigure hello Klasik dağıtım modelindeki Linux sanal makineler için kullanılabilirlik kümesi</span><span class="sxs-lookup"><span data-stu-id="0a92c-103">How tooconfigure an availability set for Linux virtual machines in hello classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="0a92c-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0a92c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0a92c-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="0a92c-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0a92c-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="0a92c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0a92c-107">Ayrıca [kullanılabilirlik kümelerini yapılandırmak](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) Resource Manager dağıtımları içinde.</span><span class="sxs-lookup"><span data-stu-id="0a92c-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]