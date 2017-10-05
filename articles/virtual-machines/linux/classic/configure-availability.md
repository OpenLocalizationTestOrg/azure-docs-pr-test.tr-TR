---
title: "Kullanılabilirlik kümeleri Klasik Linux VM'ler için | Microsoft Docs"
description: "Azure portalı ve Azure PowerShell kullanarak Klasik dağıtım modelinde yeni veya var olan Linux sanal makine için ayarlanmış kullanılabilirlik yapılandırın."
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
ms.openlocfilehash: 41d427862150d17e1ad726afc51114d6f62f5a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-an-availability-set-for-linux-virtual-machines-in-the-classic-deployment-model"></a><span data-ttu-id="16624-103">Kullanılabilirlik kümesi Klasik dağıtım modelindeki Linux sanal makineleri için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="16624-103">How to configure an availability set for Linux virtual machines in the classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="16624-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="16624-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="16624-105">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="16624-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="16624-106">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="16624-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="16624-107">Ayrıca [kullanılabilirlik kümelerini yapılandırmak](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) Resource Manager dağıtımları içinde.</span><span class="sxs-lookup"><span data-stu-id="16624-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]