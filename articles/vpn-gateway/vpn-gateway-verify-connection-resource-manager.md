---
title: "aaaVerify bir VPN ağ geçidi bağlantısı | Microsoft Docs"
description: "Bu makalede nasıl tooverify bir sanal ağ VPN ağ geçidi bağlantısı gösterilmektedir."
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
ms.openlocfilehash: 0d3da94a76b36251d629f82b1575328c7ac10b26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="55a8a-103">Bir VPN ağ geçidi bağlantısını doğrulama</span><span class="sxs-lookup"><span data-stu-id="55a8a-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="55a8a-104">Bu makale size nasıl gösterir tooverify hello Klasik ve Resource Manager dağıtım modeli için bir VPN ağ geçidi bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="55a8a-104">This article shows you how tooverify a VPN gateway connection for both hello classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="55a8a-105">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="55a8a-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="55a8a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="55a8a-106">PowerShell</span></span>

<span data-ttu-id="55a8a-107">tooverify hello Resource Manager dağıtım için bir VPN ağ geçidi bağlantısı PowerShell kullanarak model, hello hello en son sürümünü yüklemek [Azure Resource Manager PowerShell cmdlet'lerini](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="55a8a-107">tooverify a VPN gateway connection for hello Resource Manager deployment model using PowerShell, install hello latest version of hello [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="55a8a-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="55a8a-108">Azure CLI</span></span>

<span data-ttu-id="55a8a-109">tooverify hello Resource Manager dağıtım için bir VPN ağ geçidi bağlantısı Azure CLI kullanarak model, hello hello en son sürümünü yüklemek [CLI komutları](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 veya üstü).</span><span class="sxs-lookup"><span data-stu-id="55a8a-109">tooverify a VPN gateway connection for hello Resource Manager deployment model using Azure CLI, install hello latest version of hello [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="55a8a-110">Azure portal (Klasik)</span><span class="sxs-lookup"><span data-stu-id="55a8a-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="55a8a-111">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="55a8a-111">PowerShell (classic)</span></span>

<span data-ttu-id="55a8a-112">VPN ağ geçidi bağlantınızı hello Klasik dağıtım modeli PowerShell kullanarak tooverify hello hello Azure PowerShell cmdlet'lerinin en son sürümlerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="55a8a-112">tooverify your VPN gateway connection for hello classic deployment model using PowerShell, install hello latest versions of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="55a8a-113">Emin toodownload ve yükleme hello olması [Hizmet Yönetimi](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) modülü.</span><span class="sxs-lookup"><span data-stu-id="55a8a-113">Be sure toodownload and install hello [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="55a8a-114">'Add-AzureAccount' toolog toohello Klasik dağıtım modelinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="55a8a-114">Use 'Add-AzureAccount' toolog in toohello classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="55a8a-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="55a8a-115">Next steps</span></span>

* <span data-ttu-id="55a8a-116">Sanal makineler tooyour sanal ağları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55a8a-116">You can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="55a8a-117">Adımlar için bkz. [Sanal Makine Oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55a8a-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
