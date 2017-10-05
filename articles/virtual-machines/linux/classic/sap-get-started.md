---
title: SAP Linux sanal makineleri kullanma | Microsoft Docs
description: "Microsoft Azure’daki Linux sanal makinelerinde (VM) SAP çözümlerini kullanma hakkında bilgi edinin"
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 078865245989578d17b6eb0b59b379aa2056f31c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="fab5c-103">Azure'daki Linux sanal makinelerde SAP kullanma</span><span class="sxs-lookup"><span data-stu-id="fab5c-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="fab5c-104">Bulut Bilgi İşlem, BT sektöründeki küçük ölçekli şirketlerden büyük ve çok uluslu kuruluşlara kadar çok geniş ölçekte kullanılan ve her geçen gün daha önemli hale gelen bir terimdir.</span><span class="sxs-lookup"><span data-stu-id="fab5c-104">Cloud Computing is a widely used term which is gaining more and more importance within the IT industry, from small companies up to large and multinational corporations.</span></span> <span data-ttu-id="fab5c-105">Microsoft Azure, Microsoft tarafından sunulan ve birçok yeni özelliğe sahip olan Bulut Hizmetleri Platformudur.</span><span class="sxs-lookup"><span data-stu-id="fab5c-105">Microsoft Azure is the Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="fab5c-106">Bu özellikler sayesinde müşteriler artık teknik veya mali kısıtlamalara takılmadan uygulamalarını Bulut Hizmetleri olarak hazırlayabilir ve kullanımdan kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="fab5c-106">Now customers are able to rapidly provision and de-provision applications as Cloud-Services, so they are not limited to technical or budgeting restrictions.</span></span> <span data-ttu-id="fab5c-107">Şirketler, zamanlarını ve bütçelerini donanım altyapısına harcamak yerine uygulamanın kendisine, iş süreçlerine ve hem müşteriler hem de kullanıcılar için fayda sağlamaya odaklanabilir.</span><span class="sxs-lookup"><span data-stu-id="fab5c-107">Instead of investing time and budget into hardware infrastructure, companies can focus on the application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="fab5c-108">Microsoft Azure sanal makinelerle Microsoft olarak hizmet (Iaas) platform kapsamlı bir altyapı sunar.</span><span class="sxs-lookup"><span data-stu-id="fab5c-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="fab5c-109">SAP NetWeaver tabanlı uygulamalar, Azure Sanal Makinelerinde (IaaS) desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="fab5c-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="fab5c-110">Aşağıdaki teknik incelemeler, planlamanızı ve azure'da Windows sanal makinelerde SAP NetWeaver tabanlı uygulamalar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fab5c-110">The whitepapers below describe how to plan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="fab5c-111">SAP NetWeaver tabanlı uygulamalar üzerinde uygulayabilirsiniz [Windows sanal makineleri](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fab5c-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="fab5c-112">SAP NetWeaver Azure SUSE Linux sanal makinelerde</span><span class="sxs-lookup"><span data-stu-id="fab5c-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="fab5c-113">Başlık: Microsoft Azure SUSE Linux VM'ler üzerinde SAP NetWeaver test etme</span><span class="sxs-lookup"><span data-stu-id="fab5c-113">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="fab5c-114">Özet: Bu anda SAP NetWeaver Azure Linux VM'ler üzerinde çalıştırılan için resmi SAP desteği yoktur.</span><span class="sxs-lookup"><span data-stu-id="fab5c-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="fab5c-115">Yine de müşteriler bazı test yapmak isteyebileceğiniz veya SAP destek uzmanıyla gerek yoktur sürece SAP demo veya eğitim sistemleri Azure Linux VM'ler üzerinde çalıştırmak için düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fab5c-115">Nevertheless customers might want to do some testing or might consider to run SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="fab5c-116">Bu makalede Azure SUSE Linux VM'ler ayarlama SAP çalıştırmak için yardımcı olur ve ortak olası Tuzaklar önlemek için temel bazı ipuçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="fab5c-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order to avoid common potential pitfalls.</span></span>

<span data-ttu-id="fab5c-117">Güncelleştirilmiş: Aralık 2015</span><span class="sxs-lookup"><span data-stu-id="fab5c-117">Updated: December 2015</span></span>

[<span data-ttu-id="fab5c-118">Bu makalede burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="fab5c-118">This article can be found here</span></span>](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

