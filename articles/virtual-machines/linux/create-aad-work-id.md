---
title: "Bir iş veya Okul kimlik AAD'de Linux için oluşturun. | Microsoft Docs"
description: "Linux sanal makinelerinizi ile kullanmak için Azure Active Directory'de bir iş veya Okul kimlik oluşturmayı öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 4fdb72e3eec41d66f8561baf1755aa425ac278af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-to-use-with-linux-vms"></a><span data-ttu-id="b0e3e-103">Linux VM ile birlikte kullanmak için Azure Active Directory'de bir iş veya Okul kimlik oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0e3e-103">Creating a Work or School identity in Azure Active Directory to use with Linux VMs</span></span>
<span data-ttu-id="b0e3e-104">Kişisel bir Azure hesabı oluşturulduğunda veya kişisel bir MSDN aboneliğiniz ve MSDN Azure KREDİLERİ--yararlanmak için Azure hesap oluşturduğunuz kullandıysanız bir *Microsoft hesabı* kimlik oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b0e3e-104">If you created a personal Azure account or have a personal MSDN subscription and created the Azure account to take advantage of the MSDN Azure credits -- you used a *Microsoft account* identity to create it.</span></span> <span data-ttu-id="b0e3e-105">Azure--harika özelliklerinin çoğu [kaynak grubu şablonları](../../azure-resource-manager/resource-group-overview.md) bir örnek--çalışmaya (kimlik, Azure Active Directory tarafından yönetilen) bir iş veya Okul hesabı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b0e3e-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) to work.</span></span> <span data-ttu-id="b0e3e-106">Neyse ki, kişisel Azure hesabınızla ilgili en iyi özelliklerinden biri, yeni bir iş veya Okul hesabı t oluşturmak için kullanabileceğiniz varsayılan Azure Active Directory etki alanı ile birlikte gelen olduğundan yeni bir iş veya Okul hesabı oluşturmak için aşağıdaki yönergeleri izleyin hat ile gerektiren Azure özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0e3e-106">You can follow the instructions below to create a new work or school account because fortunately, one of the best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use to create a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="b0e3e-107">Ancak, en son değişiklikler Azure hesabı kullanarak herhangi bir türünü aboneliğinizle yönetmeyi kolaylaştırır `azure login` açıklanan etkileşimli oturum açma yöntemi [burada](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b0e3e-107">However, recent changes make it possible to manage your subscription with any type of Azure account using the `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="b0e3e-108">Aşağıdaki yönergeleri izleyin veya bu mekanizma ya da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0e3e-108">You can either use that mechanism, or you can follow the instructions that follow.</span></span> <span data-ttu-id="b0e3e-109">Ayrıca [Windows VM ile birlikte kullanmak için Azure Active Directory'de bir iş veya Okul kimlik oluşturmak](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0e3e-109">You can also [create a work or school identity in Azure Active Directory to use with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

