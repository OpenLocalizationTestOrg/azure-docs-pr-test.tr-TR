---
title: "bir iş veya Okul kimlik Linux için aad'de aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate Linux sanal makineleri ile Azure Active Directory toouse yer alan bir iş veya Okul kimliği."
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
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a><span data-ttu-id="227f9-103">Azure Active Directory toouse Linux VM'ler ile bir iş veya Okul kimlik oluşturma</span><span class="sxs-lookup"><span data-stu-id="227f9-103">Creating a Work or School identity in Azure Active Directory toouse with Linux VMs</span></span>
<span data-ttu-id="227f9-104">Kişisel bir Azure hesabı oluşturulduğunda veya kişisel bir MSDN aboneliğiniz ve hello Azure hesabı tootake hello MSDN Azure KREDİLERİ--avantajlarından oluşturulan kullandıysanız bir *Microsoft hesabı* kimlik toocreate onu.</span><span class="sxs-lookup"><span data-stu-id="227f9-104">If you created a personal Azure account or have a personal MSDN subscription and created hello Azure account tootake advantage of hello MSDN Azure credits -- you used a *Microsoft account* identity toocreate it.</span></span> <span data-ttu-id="227f9-105">Azure--harika özelliklerinin çoğu [kaynak grubu şablonları](../../azure-resource-manager/resource-group-overview.md) bir örnek--bir iş veya Okul hesabı (Azure Active Directory tarafından yönetilen bir kimlik) gerektirir toowork.</span><span class="sxs-lookup"><span data-stu-id="227f9-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) toowork.</span></span> <span data-ttu-id="227f9-106">Toocreate aşağıdaki Neyse ki, kişisel Azure hesabınızla ilgili hello en iyi özelliklerinden biri, yeni bir iş veya Okul toocreate kullanabileceğiniz varsayılan Azure Active Directory etki alanı ile geldiğini olduğundan yeni bir iş veya Okul hesabına hello yönergeleri izleyin gerektiren Azure özelliklerle kullandığınız hesap.</span><span class="sxs-lookup"><span data-stu-id="227f9-106">You can follow hello instructions below toocreate a new work or school account because fortunately, one of hello best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use toocreate a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="227f9-107">Ancak, son, olası toomanage değişiklik hello kullanarak Azure hesabı herhangi bir türde aboneliğinizle `azure login` açıklanan etkileşimli oturum açma yöntemi [burada](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="227f9-107">However, recent changes make it possible toomanage your subscription with any type of Azure account using hello `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="227f9-108">Bu mekanizma ya da kullanabilir veya izleyin hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="227f9-108">You can either use that mechanism, or you can follow hello instructions that follow.</span></span> <span data-ttu-id="227f9-109">Ayrıca [Windows VM'ler ile Azure Active Directory toouse bir iş veya Okul kimlik oluşturmak](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="227f9-109">You can also [create a work or school identity in Azure Active Directory toouse with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

