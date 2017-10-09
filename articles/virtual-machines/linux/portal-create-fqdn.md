---
title: "bir Linux VM hello Azure portal'ın FQDN'si aaaCreate | Microsoft Docs"
description: "Nasıl toocreate bir tam etki alanı adı veya FQDN, bir kaynak yöneticisi için sanal makine hello Azure portal'ın temel bilgi edinin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a><span data-ttu-id="c25c9-103">Bir tam etki alanı adı hello Azure portalı için bir Linux VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c25c9-103">Create a fully qualified domain name in hello Azure portal for a Linux VM</span></span>

<span data-ttu-id="c25c9-104">Bir sanal makine (VM) hello oluşturduğunuzda [Azure portal](https://portal.azure.com), genel IP kaynağı hello sanal makine için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c25c9-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="c25c9-105">Bu IP adresi tooremotely erişim hello VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="c25c9-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="c25c9-106">Merhaba portal oluşturmaz rağmen bir [tam etki alanı adı](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), veya FQDN, ekleyebileceğiniz bir hello VM oluşturulduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="c25c9-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once hello VM is created.</span></span> <span data-ttu-id="c25c9-107">Bu makalede hello adımları toocreate bir DNS adı veya FQDN gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c25c9-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="c25c9-108">Bir FQDN oluşturma</span><span class="sxs-lookup"><span data-stu-id="c25c9-108">Create a FQDN</span></span>
<span data-ttu-id="c25c9-109">Bu makale, bir VM zaten oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="c25c9-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="c25c9-110">Gerekirse, [hello Portalı'nda bir VM oluşturma](quick-create-portal.md) veya [hello Azure CLI ile](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c25c9-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with hello Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="c25c9-111">VM çalışır durumda sonra aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c25c9-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="c25c9-112">Şimdi ile bu DNS kullanarak VM adı gibi toohello uzaktan bağlanabilirsiniz `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="c25c9-112">You can now connect remotely toohello VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c25c9-113">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c25c9-113">Next steps</span></span>
<span data-ttu-id="c25c9-114">VM'yi bir ortak IP ve DNS adı olan, yaygın uygulama çerçeveleri veya nginx, MongoDB, Docker, gibi hizmetleri dağıtabilirsiniz vs.</span><span class="sxs-lookup"><span data-stu-id="c25c9-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="c25c9-115">Ayrıca daha fazla hakkında bilgiyi [Kaynak Yöneticisi'ni kullanarak](../../azure-resource-manager/resource-group-overview.md) Azure dağıtımlarınızı oluşturma ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="c25c9-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

