---
title: "Azure DevTest Labs hakkında | Microsoft Docs"
description: "Nasıl DevTest Labs oluşturmak, yönetmek ve Azure sanal makinelerini izlemek kolaylaştırmak bilgi edinin"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1b9eed3b-c69a-4c49-a36e-f388efea6f39
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 62e2d214d6d685c7f27c8c45cae161eb25ed1cbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="4a94d-103">Azure DevTest Labs hakkında</span><span class="sxs-lookup"><span data-stu-id="4a94d-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="4a94d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4a94d-104">Overview</span></span>
<span data-ttu-id="4a94d-105">Geliştiriciler ve sınayıcılar oluşturma ve buluta giderek ortamlarını yönetme gecikme çözmek için aramaktadır.</span><span class="sxs-lookup"><span data-stu-id="4a94d-105">Developers and testers are looking to solve the delays in creating and managing their environments by going to the cloud.</span></span>  <span data-ttu-id="4a94d-106">Azure ortamı gecikmeler sorununu çözer ve yeni bir maliyet verimli yapısı içinde Self Servis sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a94d-106">Azure solves the problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="4a94d-107">Ancak, geliştiriciler ve sınayıcılar hala kendi kendine sunulacak ortamlarını yapılandırma önemli ölçüde zaman ayırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a94d-107">However, developers and testers still need to spend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="4a94d-108">Ayrıca, karar alıcılar hakkında çok fazla işlem yükü eklemeden kendi maliyet tasarrufu en üst düzeye çıkarmak için bulut yararlanmak nasıl kucaklayacaklarından emin değildir.</span><span class="sxs-lookup"><span data-stu-id="4a94d-108">Also, decision makers are uncertain about how to leverage the cloud to maximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="4a94d-109">Azure DevTest Labs, geliştiricilerin yardımcı olan bir hizmettir ve sınayıcılar hızla ortamları Azure'da atık en aza indirmenizi ve maliyetini denetleme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4a94d-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="4a94d-110">Yeniden kullanılabilir şablonları ve yapıtları kullanarak Windows ve Linux ortamlarını hızla sağlayabilir ve bu sayede uygulamanızın en son sürümünü test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a94d-110">You can test the latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="4a94d-111">Kolay dağıtım hattınızı isteğe bağlı ortamları sağlamak için DevTest Labs ile tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="4a94d-111">Easily integrate your deployment pipeline with DevTest Labs to provision on-demand environments.</span></span> <span data-ttu-id="4a94d-112">Birden çok test aracılarını sağlama tarafından sınama yük ölçeklendirin ve eğitim ve gösterileri için önceden sağlandıysa ortamlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4a94d-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="4a94d-113">DevTest Labs oluşturma, yapılandırma ve bulut geliştirme ve test ortamları yönetme aşağıdaki yararları sağlar</span><span class="sxs-lookup"><span data-stu-id="4a94d-113">DevTest Labs provides the following benefits in creating, configuring, and managing developer and test environments in the cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="4a94d-114">Self Servis sorunsuz</span><span class="sxs-lookup"><span data-stu-id="4a94d-114">Worry-free self-service</span></span>
<span data-ttu-id="4a94d-115">DevTest Labs maliyetleri denetlemek için laboratuvarınız üzerinde - kullanıcı başına (VM) sanal makinelerin sayısını ve sanal makineleri laboratuvar başına gibi ilkeler ayarlamanıza olanak tanıyarak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="4a94d-115">DevTest Labs makes it easier to control costs by allowing you to set policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="4a94d-116">DevTest Labs otomatik olarak kapatmak ve sanal makineleri başlatmak için ilkeler oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a94d-116">DevTest Labs also enables you to create policies to automatically shut down and start VMs.</span></span>

## <a name="quickly-get-to-ready-to-test"></a><span data-ttu-id="4a94d-117">Hızlı bir şekilde hazır test Al</span><span class="sxs-lookup"><span data-stu-id="4a94d-117">Quickly get to ready-to-test</span></span>
<span data-ttu-id="4a94d-118">DevTest Labs, önceden hazırlanan ortamları ekibinizin geliştirme ve test uygulamaları başlatmak için gereken her şeyi ile oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a94d-118">DevTest Labs enables you to create pre-provisioned environments with everything your team needs to start developing and testing applications.</span></span> <span data-ttu-id="4a94d-119">Sadece son iyi yapılandırma, uygulamanızın yüklendiği ortamları talep ve hemen çalışmaya alın.</span><span class="sxs-lookup"><span data-stu-id="4a94d-119">Simply claim the environments where the last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="4a94d-120">Veya kapsayıcıları bile daha hızlı ve daha yalın bir ortam oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a94d-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="4a94d-121">Bir kez oluşturun, her yerde kullanın</span><span class="sxs-lookup"><span data-stu-id="4a94d-121">Create once, use everywhere</span></span>
<span data-ttu-id="4a94d-122">Yakalama ve ortam şablonları ekibinizin ve kuruluşunuzun - tüm kaynak denetiminde - içindeki yapıları Geliştirici oluşturma ve test ortamları kolayca paylaşın.</span><span class="sxs-lookup"><span data-stu-id="4a94d-122">Capture and share environment templates and artifacts within your team or organization - all in source control - to create developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="4a94d-123">Mevcut araç zinciriniz ile tümleştirilir</span><span class="sxs-lookup"><span data-stu-id="4a94d-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="4a94d-124">Önceden yapılmış eklentileri veya API'mize geliştirme ve Test ortamları için tercih edilen sürekli tümleştirme (CI) aracı doğrudan tümleşik geliştirme ortamı (IDE) ya da sürüm ardışık düzen otomatik sağlama yararlanın.</span><span class="sxs-lookup"><span data-stu-id="4a94d-124">Leverage pre-made plug-ins or our API to provision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="4a94d-125">Ayrıca bizim kapsamlı komut satırı aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a94d-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="4a94d-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4a94d-126">Next steps</span></span>
[<span data-ttu-id="4a94d-127">DevTest Labs kavramları</span><span class="sxs-lookup"><span data-stu-id="4a94d-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

