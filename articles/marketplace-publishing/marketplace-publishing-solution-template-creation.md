---
title: "aaaGuide toocreating hello Market için bir çözüm şablonu | Microsoft Docs"
description: "Nasıl toocreate, onaylamak ve hello Azure Marketi satınalma için çoklu VM görüntü çözüm şablon dağıtma ayrıntılı yönergeler için."
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
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="40adc-103">Kılavuzu toocreate Azure Market'ten bir çözüm şablonu</span><span class="sxs-lookup"><span data-stu-id="40adc-103">Guide toocreate a solution template for Azure Marketplace</span></span>
<span data-ttu-id="40adc-104">Adım 1 ' tamamladıktan sonra [hesap oluşturma ve kayıt][link-acct-creation], size bir Azure uyumlu çözüm şablon hello oluşturulmasını üzerinde destekli [oluşturmak için teknik Önkoşullar bir Çözüm şablonu](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="40adc-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on hello creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="40adc-105">Biz, hello birden çok sanal makine için bir çözüm şablonu oluşturmak için hello adımlarda size yol gösterecek artık [yayımlama portalında] [ link-pubportal] hello Azure Marketi için.</span><span class="sxs-lookup"><span data-stu-id="40adc-105">Now we will walk you through hello steps for creating a solution template for multiple VMs on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a><span data-ttu-id="40adc-106">Çözüm şablonu teklifiniz hello yayımlama Portal oluşturma</span><span class="sxs-lookup"><span data-stu-id="40adc-106">Create your solution template offer in hello Publishing Portal</span></span>
<span data-ttu-id="40adc-107">Çok Git [https://publish.windowsazure.com](http://publish.windowsazure.com). Merhaba ilk zaman toohello için oturum açarken [yayımlama portalında](https://publish.windowsazure.com/), aynı hesabı, şirketinizin satıcı profili kaydedildiği ile kullanım hello.</span><span class="sxs-lookup"><span data-stu-id="40adc-107">Go too [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for hello first time toohello [Publishing Portal](https://publish.windowsazure.com/), use hello same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="40adc-108">Daha sonra şirketinizin herhangi bir personel hello Yayımlama Portalı'nda bir ortak yönetici olarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40adc-108">Later, you can add any employee of your company as a co-admin in hello Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="40adc-109">1. "Çözüm şablonları" seçin</span><span class="sxs-lookup"><span data-stu-id="40adc-109">1. Select "Solution templates"</span></span>
  ![Çizim][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="40adc-111">2. Yeni bir çözüm şablonu oluşturun</span><span class="sxs-lookup"><span data-stu-id="40adc-111">2. Create a new solution template</span></span>
  ![Çizim][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="40adc-113">3. Topolojileri ile Başlat</span><span class="sxs-lookup"><span data-stu-id="40adc-113">3. Start with topologies</span></span>
<span data-ttu-id="40adc-114">Bir çözüm şablonu "üst" tooall topolojileri olur.</span><span class="sxs-lookup"><span data-stu-id="40adc-114">A solution template is a "parent" tooall of its topologies.</span></span> <span data-ttu-id="40adc-115">Bir teklif/çözüm şablonunda birden fazla topoloji tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40adc-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="40adc-116">Bir teklif toostaging gönderildiğinde tüm topolojileri ile gönderilir.</span><span class="sxs-lookup"><span data-stu-id="40adc-116">When an offer is pushed toostaging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="40adc-117">Teklifiniz toodefine Hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="40adc-117">Follow hello steps below toodefine your offer:</span></span>     

* <span data-ttu-id="40adc-118">Bir topoloji oluşturun: "Topolojisi tanımlayıcısı" adıdır genellikle hello hello topoloji hello çözüm şablonu için.</span><span class="sxs-lookup"><span data-stu-id="40adc-118">Create a Topology: “Topology Identifier” is typically hello name of hello topology for hello solution template.</span></span> <span data-ttu-id="40adc-119">Merhaba topolojisi tanımlayıcısı hello URL'de aşağıda gösterildiği gibi kullanılır:</span><span class="sxs-lookup"><span data-stu-id="40adc-119">hello topology identifier is used in hello URL as shown below:</span></span>

  <span data-ttu-id="40adc-120">Azure Market: http://azure.microsoft.com/marketplace/partners/ {PublisherNamespace} / {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="40adc-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="40adc-121">Azure Portal: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="40adc-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="40adc-122">Yeni bir sürüm ekleyin.</span><span class="sxs-lookup"><span data-stu-id="40adc-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="40adc-123">4. Sertifikalı topoloji sürümlerinizi Al</span><span class="sxs-lookup"><span data-stu-id="40adc-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="40adc-124">Tüm gerekli dosyaları tooprovision hello topoloji belirli bu sürümünü içeren bir zip dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="40adc-124">Upload a zip file that contains all required files tooprovision that particular version of hello topology.</span></span> <span data-ttu-id="40adc-125">Bu zip dosyası hello şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="40adc-125">This zip file must contain hello following:</span></span>

* <span data-ttu-id="40adc-126">*mainTemplate.json* ve *createUiDefinition.json* dosyasını kendi kök dizininde.</span><span class="sxs-lookup"><span data-stu-id="40adc-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="40adc-127">Tüm bağlı şablonları ve gerekli tüm betikler.</span><span class="sxs-lookup"><span data-stu-id="40adc-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="40adc-128">Geliştiricilerinize hello çözüm şablonu topolojileri oluşturmak ve bunları sertifikalı, hello iş alma üzerinde çalışırken pazarlama ve/veya yasal Departmanlar şirketinizin hello pazarlama ve yasal içerik üzerinde çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="40adc-128">While your developers work on creating hello solution template topologies and getting them certified, hello business, marketing, and/or legal departments of your company can work on hello marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="40adc-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="40adc-129">Next steps</span></span>
<span data-ttu-id="40adc-130">Çözüm şablonu oluşturduğunuz ve hello zip dosyası karşıya göre Lütfen hello hello yönergeleri izleyin [Market pazarlama içerik Kılavuzu](marketplace-publishing-push-to-staging.md) hello teklif toostaging Ftp'den önce.</span><span class="sxs-lookup"><span data-stu-id="40adc-130">Now that you created your solution template and uploaded hello zip file, please follow hello instructions in hello [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing hello offer toostaging.</span></span> <span data-ttu-id="40adc-131">toosee Market makaleler, yayımlama hello tam kümesi ziyaret [Başlarken: nasıl toopublish bir teklif toohello Azure Marketi](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="40adc-131">toosee hello full set of marketplace publishing articles, visit [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="40adc-132">Bu ilgili makalelerde ilginizi çekebilir:</span><span class="sxs-lookup"><span data-stu-id="40adc-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="40adc-133">VM görüntüleri: [azure'da sanal makine görüntülerini hakkında](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="40adc-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="40adc-134">VM uzantıları: [VM aracısı ve VM uzantılarına genel bakış](https://msdn.microsoft.com/library/azure/dn832621.aspx) ve [Azure VM uzantıları ve özellikleri](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="40adc-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="40adc-135">Azure Kaynak Yöneticisi: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md) ve [basit bir şablon örnekleri](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="40adc-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="40adc-136">Depolama hesabı kısıtlar: [nasıl tooMonitor depolama hesabı daraltması](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) ve [Premium depolama](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="40adc-136">Storage account throttles: [How tooMonitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
