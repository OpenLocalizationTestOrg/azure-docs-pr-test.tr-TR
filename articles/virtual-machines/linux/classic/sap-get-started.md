---
title: Linux sanal makinelerde SAP aaaUsing | Microsoft Docs
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
ms.openlocfilehash: a805cdecb515239057e185a92bf5c4d4e707f72f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="fb809-103">Azure'daki Linux sanal makinelerde SAP kullanma</span><span class="sxs-lookup"><span data-stu-id="fb809-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="fb809-104">Bulut bilgi işlem, daha da fazla önem hello BT endüstri içinde toolarge ve çokuluslu şirketler yukarı küçük şirketlerden elde yaygın olarak kullanılan bir terimdir.</span><span class="sxs-lookup"><span data-stu-id="fb809-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="fb809-105">Microsoft Azure hello paylaşılabilen çok sayıda yeni olanakları sunan Microsoft bulut hizmetleri platformu ' dir.</span><span class="sxs-lookup"><span data-stu-id="fb809-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="fb809-106">Değil sınırlı tootechnical veya bütçeleme kısıtlamaları; bu nedenle şimdi müşteriler mümkün toorapidly sağlama ve devre dışı bırakma sağlama bulut-Hizmetleri uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="fb809-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="fb809-107">Donanım altyapısını zamandan ve yatırım yapmak yerine, şirketler Merhaba uygulaması, iş süreçlerini ve onun avantajlarını müşteriler ve kullanıcılar için odaklanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb809-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="fb809-108">Microsoft Azure sanal makinelerle Microsoft olarak hizmet (Iaas) platform kapsamlı bir altyapı sunar.</span><span class="sxs-lookup"><span data-stu-id="fb809-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="fb809-109">SAP NetWeaver tabanlı uygulamalar, Azure Sanal Makinelerinde (IaaS) desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="fb809-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="fb809-110">Merhaba teknik incelemeler aşağıdaki nasıl tooplan ve uygulama SAP NetWeaver tabanlı uygulamaları azure'da Windows sanal makinelerde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fb809-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="fb809-111">SAP NetWeaver tabanlı uygulamalar üzerinde uygulayabilirsiniz [Windows sanal makineleri](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fb809-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="fb809-112">SAP NetWeaver Azure SUSE Linux sanal makinelerde</span><span class="sxs-lookup"><span data-stu-id="fb809-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="fb809-113">Başlık: aaaTesting SAP NetWeaver Microsoft Azure SUSE Linux sanal makineleri üzerinde</span><span class="sxs-lookup"><span data-stu-id="fb809-113">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="fb809-114">Özet: Bu anda SAP NetWeaver Azure Linux VM'ler üzerinde çalıştırılan için resmi SAP desteği yoktur.</span><span class="sxs-lookup"><span data-stu-id="fb809-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="fb809-115">Yine de müşteriler toodo bazı test isteyebilir veya SAP destek uzmanıyla gerek yoktur sürece toorun SAP demo veya eğitim sistemlerde Azure Linux VM'ler düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb809-115">Nevertheless customers might want toodo some testing or might consider toorun SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="fb809-116">Bu makalede Azure SUSE Linux VM'ler ayarlama SAP çalıştırmak için yardımcı olur ve tooavoid ortak olası Tuzaklar sırayla temel bazı ipuçları verir.</span><span class="sxs-lookup"><span data-stu-id="fb809-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order tooavoid common potential pitfalls.</span></span>

<span data-ttu-id="fb809-117">Güncelleştirilmiş: Aralık 2015</span><span class="sxs-lookup"><span data-stu-id="fb809-117">Updated: December 2015</span></span>

[<span data-ttu-id="fb809-118">Bu makalede burada bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="fb809-118">This article can be found here</span></span>](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

