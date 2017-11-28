---
title: "Bir VPN ağ geçidi bağlantısını doğrulama | Microsoft Docs"
description: "Bu makalede, bir sanal ağ VPN ağ geçidi bağlantı doğrulamak gösterilmiştir."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: b2d702ecdd5e1fca342e7c84c6e75339097f0bcd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="b51f3-103">Bir VPN ağ geçidi bağlantısını doğrulama</span><span class="sxs-lookup"><span data-stu-id="b51f3-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="b51f3-104">Bu makale VPN ağ geçidi bağlantısı Klasik ve Resource Manager dağıtım modelleri için doğrulama gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b51f3-104">This article shows you how to verify a VPN gateway connection for both the classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="b51f3-105">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="b51f3-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="b51f3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b51f3-106">PowerShell</span></span>

<span data-ttu-id="b51f3-107">PowerShell kullanarak Resource Manager dağıtım modeli için bir VPN ağ geçidi bağlantısı doğrulamak için en son sürümünü yükleyin [Azure Resource Manager PowerShell cmdlet'lerini](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b51f3-107">To verify a VPN gateway connection for the Resource Manager deployment model using PowerShell, install the latest version of the [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="b51f3-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b51f3-108">Azure CLI</span></span>

<span data-ttu-id="b51f3-109">Azure CLI kullanarak Resource Manager dağıtım modeli için bir VPN ağ geçidi bağlantısı doğrulamak için en son sürümünü yükleyin [CLI komutları](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 veya üstü).</span><span class="sxs-lookup"><span data-stu-id="b51f3-109">To verify a VPN gateway connection for the Resource Manager deployment model using Azure CLI, install the latest version of the [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="b51f3-110">Azure portal (Klasik)</span><span class="sxs-lookup"><span data-stu-id="b51f3-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="b51f3-111">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="b51f3-111">PowerShell (classic)</span></span>

<span data-ttu-id="b51f3-112">VPN ağ geçidi bağlantınızı PowerShell kullanarak Klasik dağıtım modeli için doğrulamak için Azure PowerShell cmdlet'lerinin en son sürümlerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b51f3-112">To verify your VPN gateway connection for the classic deployment model using PowerShell, install the latest versions of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="b51f3-113">İndirmek ve yüklemek mutlaka [Hizmet Yönetimi](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) modülü.</span><span class="sxs-lookup"><span data-stu-id="b51f3-113">Be sure to download and install the [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="b51f3-114">Klasik dağıtım modeli için oturum açmak için 'Add-AzureAccount' kullanın.</span><span class="sxs-lookup"><span data-stu-id="b51f3-114">Use 'Add-AzureAccount' to log in to the classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b51f3-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b51f3-115">Next steps</span></span>

* <span data-ttu-id="b51f3-116">Sanal ağlarınıza sanal makineler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b51f3-116">You can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="b51f3-117">Adımlar için bkz. [Sanal Makine Oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b51f3-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>