---
title: "aaaCreate hello Azure portal'ın Windows VM için FQDN | Microsoft Docs"
description: "Nasıl toocreate bir tam etki alanı adı veya FQDN, bir kaynak yöneticisi için sanal makine hello Azure portal'ın temel bilgi edinin."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a><span data-ttu-id="cd96c-103">Bir tam etki alanı adı için bir Windows VM hello Azure portal oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd96c-103">Create a fully qualified domain name in hello Azure portal for a Windows VM</span></span>

<span data-ttu-id="cd96c-104">Bir sanal makine (VM) hello oluşturduğunuzda [Azure portal](https://portal.azure.com), genel IP kaynağı hello sanal makine için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cd96c-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="cd96c-105">Bu IP adresi tooremotely erişim hello VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="cd96c-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="cd96c-106">Merhaba portal oluşturmaz rağmen bir [tam etki alanı adı](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), veya FQDN, oluşturabilmeniz hello VM oluşturulduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="cd96c-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once hello VM is created.</span></span> <span data-ttu-id="cd96c-107">Bu makalede hello adımları toocreate bir DNS adı veya FQDN gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cd96c-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="cd96c-108">Bir FQDN oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd96c-108">Create a FQDN</span></span>
<span data-ttu-id="cd96c-109">Bu makale, bir VM zaten oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="cd96c-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="cd96c-110">Gerekirse, [hello Portalı'nda bir VM oluşturma](quick-create-portal.md) veya [Azure PowerShell ile](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cd96c-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="cd96c-111">VM çalışır durumda sonra aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="cd96c-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="cd96c-112">Bu DNS adı gibi Uzak Masaüstü Protokolü (RDP) kullanarak VM toohello artık uzaktan bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd96c-112">You can now connect remotely toohello VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd96c-113">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cd96c-113">Next steps</span></span>
<span data-ttu-id="cd96c-114">Bir ortak IP ve DNS adı, VM sahip, ortak uygulama çerçeveleri veya IIS, SQL ve SharePoint gibi hizmetleri dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd96c-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="cd96c-115">Ayrıca daha fazla hakkında bilgiyi [Kaynak Yöneticisi'ni kullanarak](../../azure-resource-manager/resource-group-overview.md) Azure dağıtımlarınızı oluşturma ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="cd96c-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

