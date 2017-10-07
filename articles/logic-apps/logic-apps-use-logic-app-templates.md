---
title: "Şablonları - Azure Logic Apps aaaCreate akışlarından | Microsoft Docs"
description: "Kullanmaya başlama - Azure mantıksal uygulama şablonları tooconnect uygulamaları kullanarak hızlı bir şekilde iş akışları oluşturmak ve veri tümleştirebilirsiniz."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0127523662a12076772b52968f1e2f9cbad72a1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-tooget-started-quickly"></a><span data-ttu-id="01899-103">Önceden derlenmiş şablon veya hızlı şekilde kullanmaya düzeni tooget kullanarak bir iş akışı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="01899-103">Configure a workflow using a pre-built template or pattern tooget started quickly</span></span>

## <a name="what-are-logic-app-templates"></a><span data-ttu-id="01899-104">Mantıksal uygulama şablonları nelerdir</span><span class="sxs-lookup"><span data-stu-id="01899-104">What are logic app templates</span></span>
<span data-ttu-id="01899-105">Bir mantıksal uygulama tooquickly kullanabileceğiniz önceden oluşturulmuş mantıksal uygulama kendi iş akışı oluşturma Başlarken şablonudur.</span><span class="sxs-lookup"><span data-stu-id="01899-105">A logic app template is a pre-built logic app that you can use tooquickly get started creating your own workflow.</span></span> 

<span data-ttu-id="01899-106">Bu şablonlar logic apps kullanarak yerleşik çeşitli desenleri en iyi yolu toodiscover alır.</span><span class="sxs-lookup"><span data-stu-id="01899-106">These templates are a good way toodiscover various patterns that can be built using logic apps.</span></span> <span data-ttu-id="01899-107">Bu şablon olarak da kullanabilirsiniz-toofit değiştirin ya da senaryonuz.</span><span class="sxs-lookup"><span data-stu-id="01899-107">You can either use these templates as-is or modify them toofit your scenario.</span></span>

## <a name="overview-of-available-templates"></a><span data-ttu-id="01899-108">Kullanılabilir şablonlarına genel bakış</span><span class="sxs-lookup"><span data-stu-id="01899-108">Overview of available templates</span></span>
<span data-ttu-id="01899-109">Şu anda hello mantığı uygulama platformu yayımlanan birçok kullanılabilir şablonlar vardır.</span><span class="sxs-lookup"><span data-stu-id="01899-109">There are many available templates currently published in hello logic app platform.</span></span> <span data-ttu-id="01899-110">Bazı örnek kategorileri yanı sıra bunların içinde kullanılan bağlayıcılar hello türü aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="01899-110">Some example categories, as well as hello type of connectors used in them, are listed below.</span></span>

### <a name="enterprise-cloud-templates"></a><span data-ttu-id="01899-111">Kurumsal bulut şablonlar</span><span class="sxs-lookup"><span data-stu-id="01899-111">Enterprise cloud templates</span></span>
<span data-ttu-id="01899-112">Dynamics CRM, Salesforce, kutusu, Azure Blob ve kurumsal bulut gereksinimleriniz için diğer bağlayıcıları tümleştirmek şablonları.</span><span class="sxs-lookup"><span data-stu-id="01899-112">Templates that integrate Dynamics CRM, Salesforce, Box, Azure Blob, and other connectors for your enterprise cloud needs.</span></span> <span data-ttu-id="01899-113">Bazı örnekler ne bunlarla yapılabilir şablonları, müşteri adayları düzenleme ve kurumsal dosya verilerinizi yedeklemeye içerir.</span><span class="sxs-lookup"><span data-stu-id="01899-113">Some examples of what can be done with these templates include organizing your leads and backing up your corporate file data.</span></span>

### <a name="enterprise-integration-pack-templates"></a><span data-ttu-id="01899-114">Kurumsal tümleştirme paketi şablonları</span><span class="sxs-lookup"><span data-stu-id="01899-114">Enterprise integration pack templates</span></span>
<span data-ttu-id="01899-115">VETER yapılandırmalarını (doğrulamak, ayıklama, dönüştürme, zenginleştirmek ve rota) ardışık EDI belge AS2 üzerinde ve tooXML, dönüştürme olarak yanı sıra X12 ve AS2 iletisi olarak işleme bir X12 alma.</span><span class="sxs-lookup"><span data-stu-id="01899-115">Configurations of VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming it tooXML, as well as X12 and AS2 message handling.</span></span>

### <a name="protocol-pattern-templates"></a><span data-ttu-id="01899-116">Protokol düzeni şablonları</span><span class="sxs-lookup"><span data-stu-id="01899-116">Protocol pattern templates</span></span>
<span data-ttu-id="01899-117">İstek-yanıt gibi Protokolü düzenleri tümleştirmeler yanı sıra HTTP FTP ve SFTP arasında içeren mantıksal uygulamalar, bu şablonları oluşur.</span><span class="sxs-lookup"><span data-stu-id="01899-117">These templates consist of logic apps that contain protocol patterns such as request-response over HTTP as well as integrations across FTP and SFTP.</span></span> <span data-ttu-id="01899-118">Bunlar oldukları gibi veya temel olarak daha karmaşık Protokolü desenleri oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="01899-118">Use these as they exist, or as a basis for creating more complex protocol patterns.</span></span>  

### <a name="personal-productivity-templates"></a><span data-ttu-id="01899-119">Kişisel üretkenlik şablonları</span><span class="sxs-lookup"><span data-stu-id="01899-119">Personal productivity templates</span></span>
<span data-ttu-id="01899-120">Desenler toohelp kişisel üretkenliği artırmak günlük anımsatıcı ayarı, yapılacaklar listelerinde önemli iş öğelerini açın ve tooa tek kullanıcı onayı adım uzun görevleri otomatikleştirmek şablonları içerir.</span><span class="sxs-lookup"><span data-stu-id="01899-120">Patterns toohelp improve personal productivity include templates that set daily reminders, turn important work items into to-do lists, and automate lengthy tasks down tooa single user approval step.</span></span>

### <a name="consumer-cloud-templates"></a><span data-ttu-id="01899-121">Tüketici bulut şablonları</span><span class="sxs-lookup"><span data-stu-id="01899-121">Consumer cloud templates</span></span>
<span data-ttu-id="01899-122">Twitter, boşluk ve e-posta, sosyal medya girişimleri pazarlama güçlendirme sonuçta özellikli gibi sosyal medya Hizmetleri ile tümleştirme basit şablonları.</span><span class="sxs-lookup"><span data-stu-id="01899-122">Simple templates that integrate with social media services such as Twitter, Slack, and email, ultimately capable of strengthening social media marketing initiatives.</span></span> <span data-ttu-id="01899-123">Bu da üretkenliklerini geleneksel yinelenen görevler üzerinde harcanan süre kaydederek yardımcı olabilecek cloudy kopyalama gibi şablonları içerir.</span><span class="sxs-lookup"><span data-stu-id="01899-123">These also include templates such as cloudy copying, which can help increase productivity by saving time spent on traditionally repetitive tasks.</span></span> 

## <a name="how-toocreate-a-logic-app-using-a-template"></a><span data-ttu-id="01899-124">Nasıl toocreate bir şablonu kullanarak bir mantıksal uygulama</span><span class="sxs-lookup"><span data-stu-id="01899-124">How toocreate a logic app using a template</span></span>
<span data-ttu-id="01899-125">bir mantıksal uygulama şablonu kullanmaya tooget hello mantığı Uygulama Tasarımcısı'na gidin.</span><span class="sxs-lookup"><span data-stu-id="01899-125">tooget started using a logic app template, go into hello logic app designer.</span></span> <span data-ttu-id="01899-126">Varolan bir mantıksal uygulama açarak hello Tasarımcısı girdiğinizden yoksa, hello mantıksal Uygulama Tasarımcısı görünümünüzde otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="01899-126">If you're entering hello designer by opening an existing logic app, hello logic app automatically loads in your designer view.</span></span> <span data-ttu-id="01899-127">Ancak, yeni bir mantıksal uygulama oluşturuyorsanız, aşağıdaki hello ekrana bakın.</span><span class="sxs-lookup"><span data-stu-id="01899-127">However, if you're creating a new logic app, you see hello screen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

<span data-ttu-id="01899-128">Bu ekranda toostart boş mantıksal uygulama ya da önceden derlenmiş şablon ile ya da seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01899-128">From this screen, you can either choose toostart with a blank logic app or a pre-built template.</span></span> <span data-ttu-id="01899-129">Merhaba şablonlarından birini seçerseniz, ek bilgiler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="01899-129">If you select one of hello templates, you are provided with additional information.</span></span> <span data-ttu-id="01899-130">Bu örnekte, kullandığımız hello *yeni bir dosya Dropbox'oluşturulduğunda, tooOneDrive kopyalama* şablonu.</span><span class="sxs-lookup"><span data-stu-id="01899-130">In this example, we use hello *When a new file is created in Dropbox, copy it tooOneDrive* template.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

<span data-ttu-id="01899-131">Merhaba toouse hello şablonu seçerseniz, yalnızca seçin *bu şablonu kullanmak* düğmesi.</span><span class="sxs-lookup"><span data-stu-id="01899-131">If you choose toouse hello template, just select hello *use this template* button.</span></span> <span data-ttu-id="01899-132">Hangi bağlayıcılar hello şablonu kullanan temel tooyour hesaplarındaki toosign istenir.</span><span class="sxs-lookup"><span data-stu-id="01899-132">You'll be asked toosign in tooyour accounts based on which connectors hello template utilizes.</span></span> <span data-ttu-id="01899-133">Ya da daha önce bu bağlayıcıların bağlantıyla belirlediğinize göre seçebileceğiniz aşağıda görüldüğü gibi devam eder.</span><span class="sxs-lookup"><span data-stu-id="01899-133">Or, if you've previously established a connection with these connectors, you can select continue as seen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

<span data-ttu-id="01899-134">Merhaba bağlantı kurma ve seçtikten sonra *devam*, hello mantıksal Uygulama Tasarımcısı görünümünde açılır.</span><span class="sxs-lookup"><span data-stu-id="01899-134">After establishing hello connection and selecting *continue*, hello logic app opens in designer view.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

<span data-ttu-id="01899-135">Birçok şablonlarıyla Hello olduğu gibi hello yukarıdaki örnekte, bazı hello zorunlu özellik alanlarını hello bağlayıcılar içinde doldurulması; Ancak, bazı hala bir değer bölümlemeye önce gerektirebilir tooproperly hello mantıksal uygulama dağıtın.</span><span class="sxs-lookup"><span data-stu-id="01899-135">In hello example above, as is hello case with many templates, some of hello mandatory property fields may be filled out within hello connectors; however, some might still require a value before being able tooproperly deploy hello logic app.</span></span> <span data-ttu-id="01899-136">Bazı alanlar eksik hello girmeden toodeploy çalışırsanız, bir hata iletisi ile bildirilir.</span><span class="sxs-lookup"><span data-stu-id="01899-136">If you try toodeploy without entering some of hello missing fields, you'll be notified with an error message.</span></span>

<span data-ttu-id="01899-137">Merhaba tooreturn toohello şablonu Görüntüleyicisi istiyorsanız seçin *şablonları* hello üst gezinti çubuğu düğmesini.</span><span class="sxs-lookup"><span data-stu-id="01899-137">If you wish tooreturn toohello template viewer, select hello *Templates* button in hello top navigation bar.</span></span> <span data-ttu-id="01899-138">Geri toohello şablonu Görüntüleyicisi geçerek, kaydedilmemiş ilerleme kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="01899-138">By switching back toohello template viewer, you lose any unsaved progress.</span></span> <span data-ttu-id="01899-139">Önceki tooswitching şablonu Görüntüleyicisi uygulamasına geri bu bildiren bir uyarı iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="01899-139">Prior tooswitching back into template viewer, you'll see a warning message notifying you of this.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-toodeploy-a-logic-app-created-from-a-template"></a><span data-ttu-id="01899-140">Nasıl bir mantıksal uygulama toodeploy şablondan oluşturulan</span><span class="sxs-lookup"><span data-stu-id="01899-140">How toodeploy a logic app created from a template</span></span>
<span data-ttu-id="01899-141">Şablonunuzu yüklü ve istediğiniz değişiklikleri yapılan sonra Kaydet düğmesine hello hello sol üst köşedeki seçin.</span><span class="sxs-lookup"><span data-stu-id="01899-141">Once you have loaded your template and made any desired changes, select hello save button in hello upper left corner.</span></span> <span data-ttu-id="01899-142">Bu kaydeder ve mantıksal uygulamanızı yayımlar.</span><span class="sxs-lookup"><span data-stu-id="01899-142">This saves and publishes your logic app.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

<span data-ttu-id="01899-143">İster nasıl tooadd var olan bir mantıksal uygulama şablonu daha adımları hakkında daha fazla bilgi veya genel düzenlemeler, hakkında daha fazla okuma [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="01899-143">If you would like more information on how tooadd more steps into an existing logic app template, or make edits in general, read more at [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

