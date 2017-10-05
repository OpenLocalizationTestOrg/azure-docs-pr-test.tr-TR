---
title: "Market bir çözüm şablonu oluşturmak için kılavuz | Microsoft Docs"
description: "Oluşturma, onaylamak ve dağıtmak için bir çoklu VM görüntü çözüm şablonu konusunda ayrıntılı yönergeler Azure Market satın alın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b753bfb4bd69bd9aacf4eebd8999397394c28bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="8ece2-103">Azure Market'ten bir çözüm şablonu oluşturmak için kılavuz</span><span class="sxs-lookup"><span data-stu-id="8ece2-103">Guide to create a solution template for Azure Marketplace</span></span>
<span data-ttu-id="8ece2-104">Adım 1 ' tamamladıktan sonra [hesap oluşturma ve kayıt][link-acct-creation], bir Azure uyumlu çözüm şablon oluşturma işleminde size kılavuzluk [oluşturmak için teknik Önkoşullar bir Çözüm şablonu](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="8ece2-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on the creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="8ece2-105">Biz, üzerinde birden çok VM için bir çözüm şablonu oluşturmak için adımlarda size yol gösterecek artık [yayımlama portalında] [ link-pubportal] Azure Marketi için.</span><span class="sxs-lookup"><span data-stu-id="8ece2-105">Now we will walk you through the steps for creating a solution template for multiple VMs on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-the-publishing-portal"></a><span data-ttu-id="8ece2-106">Çözüm şablonu teklifiniz yayımlama portalında oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ece2-106">Create your solution template offer in the Publishing Portal</span></span>
<span data-ttu-id="8ece2-107">Git [https://publish.windowsazure.com](http://publish.windowsazure.com). İlk kez oturum açarken [yayımlama portalında](https://publish.windowsazure.com/), aynı hesabı, şirketinizin satıcı profili kaydedildiği ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="8ece2-107">Go to  [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for the first time to the [Publishing Portal](https://publish.windowsazure.com/), use the same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="8ece2-108">Daha sonra şirketinizin herhangi bir personel yayımlama portalında ortak yönetici olarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ece2-108">Later, you can add any employee of your company as a co-admin in the Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="8ece2-109">1. "Çözüm şablonları" seçin</span><span class="sxs-lookup"><span data-stu-id="8ece2-109">1. Select "Solution templates"</span></span>
  ![Çizim][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="8ece2-111">2. Yeni bir çözüm şablonu oluşturun</span><span class="sxs-lookup"><span data-stu-id="8ece2-111">2. Create a new solution template</span></span>
  ![Çizim][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="8ece2-113">3. Topolojileri ile Başlat</span><span class="sxs-lookup"><span data-stu-id="8ece2-113">3. Start with topologies</span></span>
<span data-ttu-id="8ece2-114">Bir çözüm şablonu tüm topolojilerinin "üst öğesidir".</span><span class="sxs-lookup"><span data-stu-id="8ece2-114">A solution template is a "parent" to all of its topologies.</span></span> <span data-ttu-id="8ece2-115">Bir teklif/çözüm şablonunda birden fazla topoloji tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ece2-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="8ece2-116">Bir teklif hazırlama için gönderildiğinde tüm topolojileri ile birlikte iletilir.</span><span class="sxs-lookup"><span data-stu-id="8ece2-116">When an offer is pushed to staging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="8ece2-117">Teklifiniz tanımlamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8ece2-117">Follow the steps below to define your offer:</span></span>     

* <span data-ttu-id="8ece2-118">Bir topoloji oluşturun: "topoloji" tanımlayıcısıdır genellikle çözüm şablonu için topoloji adı.</span><span class="sxs-lookup"><span data-stu-id="8ece2-118">Create a Topology: “Topology Identifier” is typically the name of the topology for the solution template.</span></span> <span data-ttu-id="8ece2-119">Topoloji tanımlayıcı URL'de aşağıda gösterildiği gibi kullanılır:</span><span class="sxs-lookup"><span data-stu-id="8ece2-119">The topology identifier is used in the URL as shown below:</span></span>

  <span data-ttu-id="8ece2-120">Azure Market: http://azure.microsoft.com/marketplace/partners/ {PublisherNamespace} / {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="8ece2-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="8ece2-121">Azure Portal: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="8ece2-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="8ece2-122">Yeni bir sürüm ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8ece2-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="8ece2-123">4. Sertifikalı topoloji sürümlerinizi Al</span><span class="sxs-lookup"><span data-stu-id="8ece2-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="8ece2-124">Bu belirli sürümü topolojisinin sağlamak için tüm gerekli dosyaları içeren bir zip dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8ece2-124">Upload a zip file that contains all required files to provision that particular version of the topology.</span></span> <span data-ttu-id="8ece2-125">Bu zip dosyası şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="8ece2-125">This zip file must contain the following:</span></span>

* <span data-ttu-id="8ece2-126">*mainTemplate.json* ve *createUiDefinition.json* dosyasını kendi kök dizininde.</span><span class="sxs-lookup"><span data-stu-id="8ece2-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="8ece2-127">Tüm bağlı şablonları ve gerekli tüm betikler.</span><span class="sxs-lookup"><span data-stu-id="8ece2-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="8ece2-128">Geliştiricilere çözüm şablonu topolojileri oluşturmak ve bunları sertifikalı, iş alma üzerinde çalışırken pazarlama ve/veya yasal Departmanlar şirketinizin pazarlama ve yasal içerik üzerinde çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="8ece2-128">While your developers work on creating the solution template topologies and getting them certified, the business, marketing, and/or legal departments of your company can work on the marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="8ece2-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ece2-129">Next steps</span></span>
<span data-ttu-id="8ece2-130">Çözüm şablonu oluşturduğunuz ve zip dosyası karşıya göre Lütfen'ndaki yönergeleri izleyin [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) teklif hazırlama için itme önce.</span><span class="sxs-lookup"><span data-stu-id="8ece2-130">Now that you created your solution template and uploaded the zip file, please follow the instructions in the [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing the offer to staging.</span></span> <span data-ttu-id="8ece2-131">Market makaleleri yayımlama, tamamını görmek için ziyaret [Başlarken: bir teklifi Azure Marketinde yayımlama](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="8ece2-131">To see the full set of marketplace publishing articles, visit [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="8ece2-132">Bu ilgili makalelerde ilginizi çekebilir:</span><span class="sxs-lookup"><span data-stu-id="8ece2-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="8ece2-133">VM görüntüleri: [azure'da sanal makine görüntülerini hakkında](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="8ece2-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="8ece2-134">VM uzantıları: [VM aracısı ve VM uzantılarına genel bakış](https://msdn.microsoft.com/library/azure/dn832621.aspx) ve [Azure VM uzantıları ve özellikleri](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="8ece2-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="8ece2-135">Azure Kaynak Yöneticisi: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md) ve [basit bir şablon örnekleri](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="8ece2-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="8ece2-136">Depolama hesabı kısıtlar: [izleme depolama hesabı daraltması](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) ve [Premium depolama](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="8ece2-136">Storage account throttles: [How to Monitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
