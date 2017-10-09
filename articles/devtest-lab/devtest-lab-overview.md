---
title: Azure DevTest Labs aaaAbout | Microsoft Docs
description: "Nasıl DevTest Labs kolay toocreate olun, yönetebilir ve Azure sanal makinelerini izlemek öğrenin"
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
ms.openlocfilehash: 5e5aa683f80144a2f6872c7fa328016120ea6253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-devtest-labs"></a><span data-ttu-id="0055a-103">Azure DevTest Labs hakkında</span><span class="sxs-lookup"><span data-stu-id="0055a-103">About Azure DevTest Labs</span></span>
## <a name="overview"></a><span data-ttu-id="0055a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0055a-104">Overview</span></span>
<span data-ttu-id="0055a-105">Geliştiriciler ve sınayıcılar toosolve hello gecikmeler oluşturma ve toohello bulut giderek ortamlarını yönetme aramaktadır.</span><span class="sxs-lookup"><span data-stu-id="0055a-105">Developers and testers are looking toosolve hello delays in creating and managing their environments by going toohello cloud.</span></span>  <span data-ttu-id="0055a-106">Azure ortamı gecikmeler hello sorununu çözer ve yeni bir maliyet verimli yapısı içinde Self Servis sağlar.</span><span class="sxs-lookup"><span data-stu-id="0055a-106">Azure solves hello problem of environment delays and allows self-service within a new cost efficient structure.</span></span>  <span data-ttu-id="0055a-107">Ancak, geliştiriciler ve sınayıcılar hala toospend önemli ölçüde zaman kendi kendine sunulacak ortamlarını yapılandırma gerekir.</span><span class="sxs-lookup"><span data-stu-id="0055a-107">However, developers and testers still need toospend considerable time configuring their self-served environments.</span></span> <span data-ttu-id="0055a-108">Ayrıca, karar alıcılar tooleverage hello bulut toomaximize eklemeden kendi maliyet tasarrufu çok yükü işleminin nasıl hakkında kesin değildir.</span><span class="sxs-lookup"><span data-stu-id="0055a-108">Also, decision makers are uncertain about how tooleverage hello cloud toomaximize their cost savings without adding too much process overhead.</span></span>

<span data-ttu-id="0055a-109">Azure DevTest Labs, geliştiricilerin yardımcı olan bir hizmettir ve sınayıcılar hızla ortamları Azure'da atık en aza indirmenizi ve maliyetini denetleme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0055a-109">Azure DevTest Labs is a service that helps developers and testers quickly create environments in Azure while minimizing waste and controlling cost.</span></span> <span data-ttu-id="0055a-110">Yeniden kullanılabilir şablonlar ve yapıları kullanarak Windows ve Linux ortamlar hızlı sağlama tarafından hello en son sürümü, uygulamanızın test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0055a-110">You can test hello latest version of your application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span> <span data-ttu-id="0055a-111">Kolay dağıtım hattınızı DevTest Labs tooprovision isteğe bağlı ortamlarıyla tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="0055a-111">Easily integrate your deployment pipeline with DevTest Labs tooprovision on-demand environments.</span></span> <span data-ttu-id="0055a-112">Birden çok test aracılarını sağlama tarafından sınama yük ölçeklendirin ve eğitim ve gösterileri için önceden sağlandıysa ortamlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0055a-112">Scale up your load testing by provisioning multiple test agents, and create pre-provisioned environments for training and demos.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/What-is-Azure-DevTest-Labs/player]
> 
> 

<span data-ttu-id="0055a-113">DevTest Labs oluşturma, yapılandırma ve geliştirici ve test ortamları hello bulutta yönetme avantajlarından aşağıdaki hello sağlar</span><span class="sxs-lookup"><span data-stu-id="0055a-113">DevTest Labs provides hello following benefits in creating, configuring, and managing developer and test environments in hello cloud</span></span>

## <a name="worry-free-self-service"></a><span data-ttu-id="0055a-114">Self Servis sorunsuz</span><span class="sxs-lookup"><span data-stu-id="0055a-114">Worry-free self-service</span></span>
<span data-ttu-id="0055a-115">DevTest Labs daha kolay toocontrol maliyetleri tooset ilkeleri - sanal makine (VM) sayısı gibi Laboratuvarınızı üzerinde sağlayarak kullanıcı ve VM'lerin sayısını Laboratuvar başına başına kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="0055a-115">DevTest Labs makes it easier toocontrol costs by allowing you tooset policies on your lab - such as number of virtual machines (VM) per user and number of VMs per lab.</span></span> <span data-ttu-id="0055a-116">DevTest Labs ayrıca kapatmak, toocreate ilkeleri tooautomatically sağlar ve sanal makineleri başlatın.</span><span class="sxs-lookup"><span data-stu-id="0055a-116">DevTest Labs also enables you toocreate policies tooautomatically shut down and start VMs.</span></span>

## <a name="quickly-get-tooready-to-test"></a><span data-ttu-id="0055a-117">Hızlı bir şekilde tooready test Al</span><span class="sxs-lookup"><span data-stu-id="0055a-117">Quickly get tooready-to-test</span></span>
<span data-ttu-id="0055a-118">DevTest Labs toocreate önceden sağlanan ortamlarıyla ekibinizin geliştirmek ve uygulamalarını test etme toostart gereken her şeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0055a-118">DevTest Labs enables you toocreate pre-provisioned environments with everything your team needs toostart developing and testing applications.</span></span> <span data-ttu-id="0055a-119">Sadece hello son iyi yapılandırma, uygulamanızın yüklendiği hello ortamları talep ve hemen çalışmaya alın.</span><span class="sxs-lookup"><span data-stu-id="0055a-119">Simply claim hello environments where hello last good build of your application is installed and get working right away.</span></span> <span data-ttu-id="0055a-120">Veya kapsayıcıları bile daha hızlı ve daha yalın bir ortam oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0055a-120">Or, use containers for even faster and leaner environment creation.</span></span>

## <a name="create-once-use-everywhere"></a><span data-ttu-id="0055a-121">Bir kez oluşturun, her yerde kullanın</span><span class="sxs-lookup"><span data-stu-id="0055a-121">Create once, use everywhere</span></span>
<span data-ttu-id="0055a-122">Yakalama ortamı şablonları ve yapıları ekibinizin ve kuruluşunuzun - tüm kaynak denetiminde - içinde toocreate Geliştirici paylaşabilir ve kolayca sınama ortamlarında.</span><span class="sxs-lookup"><span data-stu-id="0055a-122">Capture and share environment templates and artifacts within your team or organization - all in source control - toocreate developer and test environments easily.</span></span>

## <a name="integrates-with-your-existing-toolchain"></a><span data-ttu-id="0055a-123">Mevcut araç zinciriniz ile tümleştirilir</span><span class="sxs-lookup"><span data-stu-id="0055a-123">Integrates with your existing toolchain</span></span>
<span data-ttu-id="0055a-124">Önceden yapılmış eklentileri yararlanan veya doğrudan sunduğumuz API tooprovision geliştirme ve Test ortamları, tercih edilen sürekli tümleştirme (CI) aracından tümleşik geliştirme ortamı (IDE) veya yayın ardışık düzen otomatik.</span><span class="sxs-lookup"><span data-stu-id="0055a-124">Leverage pre-made plug-ins or our API tooprovision Dev/Test environments directly from your preferred continuous integration (CI) tool, integrated development environment (IDE), or automated release pipeline.</span></span> <span data-ttu-id="0055a-125">Ayrıca bizim kapsamlı komut satırı aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0055a-125">You can also use our comprehensive command-line tool.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="0055a-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0055a-126">Next steps</span></span>
[<span data-ttu-id="0055a-127">DevTest Labs kavramları</span><span class="sxs-lookup"><span data-stu-id="0055a-127">DevTest Labs concepts</span></span>](devtest-lab-concepts.md)

