---
title: "İş akışları şablonlardan - Azure Logic Apps oluşturmak | Microsoft Docs"
description: "Kullanmaya başlama - uygulamaları bağlamak ve veri tümleştirmek için Azure mantıksal uygulama şablonları kullanarak iş akışlarını hızla oluşturun."
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
ms.openlocfilehash: 89272869f7dfaa34cbd2ad32d67dca0955e6158b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-to-get-started-quickly"></a><span data-ttu-id="12a7d-103">Hızlıca başlamak için önceden derlenmiş şablon veya desen kullanarak bir iş akışı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="12a7d-103">Configure a workflow using a pre-built template or pattern to get started quickly</span></span>

## <a name="what-are-logic-app-templates"></a><span data-ttu-id="12a7d-104">Mantıksal uygulama şablonları nelerdir</span><span class="sxs-lookup"><span data-stu-id="12a7d-104">What are logic app templates</span></span>
<span data-ttu-id="12a7d-105">Bir mantıksal uygulama şablonu, hızlı bir şekilde kendi iş akışı oluşturmaya başlamak için kullanabileceğiniz önceden oluşturulmuş mantıksal uygulama ' dir.</span><span class="sxs-lookup"><span data-stu-id="12a7d-105">A logic app template is a pre-built logic app that you can use to quickly get started creating your own workflow.</span></span> 

<span data-ttu-id="12a7d-106">Bu şablonlar, logic apps kullanarak yerleşik çeşitli desenlerini bulmak için iyi bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="12a7d-106">These templates are a good way to discover various patterns that can be built using logic apps.</span></span> <span data-ttu-id="12a7d-107">Bu şablon olarak da kullanabilirsiniz- ya da bunları senaryonuza uyacak şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="12a7d-107">You can either use these templates as-is or modify them to fit your scenario.</span></span>

## <a name="overview-of-available-templates"></a><span data-ttu-id="12a7d-108">Kullanılabilir şablonlarına genel bakış</span><span class="sxs-lookup"><span data-stu-id="12a7d-108">Overview of available templates</span></span>
<span data-ttu-id="12a7d-109">Şu anda logic app platform yayımlanan birçok kullanılabilir şablonlar vardır.</span><span class="sxs-lookup"><span data-stu-id="12a7d-109">There are many available templates currently published in the logic app platform.</span></span> <span data-ttu-id="12a7d-110">Bazı örnek kategorileri yanı sıra bunların içinde kullanılan bağlayıcılar türünü aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="12a7d-110">Some example categories, as well as the type of connectors used in them, are listed below.</span></span>

### <a name="enterprise-cloud-templates"></a><span data-ttu-id="12a7d-111">Kurumsal bulut şablonlar</span><span class="sxs-lookup"><span data-stu-id="12a7d-111">Enterprise cloud templates</span></span>
<span data-ttu-id="12a7d-112">Dynamics CRM, Salesforce, kutusu, Azure Blob ve kurumsal bulut gereksinimleriniz için diğer bağlayıcıları tümleştirmek şablonları.</span><span class="sxs-lookup"><span data-stu-id="12a7d-112">Templates that integrate Dynamics CRM, Salesforce, Box, Azure Blob, and other connectors for your enterprise cloud needs.</span></span> <span data-ttu-id="12a7d-113">Bazı örnekler ne bunlarla yapılabilir şablonları, müşteri adayları düzenleme ve kurumsal dosya verilerinizi yedeklemeye içerir.</span><span class="sxs-lookup"><span data-stu-id="12a7d-113">Some examples of what can be done with these templates include organizing your leads and backing up your corporate file data.</span></span>

### <a name="enterprise-integration-pack-templates"></a><span data-ttu-id="12a7d-114">Kurumsal tümleştirme paketi şablonları</span><span class="sxs-lookup"><span data-stu-id="12a7d-114">Enterprise integration pack templates</span></span>
<span data-ttu-id="12a7d-115">VETER yapılandırmalarını (doğrulamak, ayıklama, dönüştürme, zenginleştirmek ve rota) ardışık EDI belge AS2 üzerinde ve XML için dönüştürme olarak yanı sıra X12 ve AS2 iletisi olarak işleme bir X12 alma.</span><span class="sxs-lookup"><span data-stu-id="12a7d-115">Configurations of VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming it to XML, as well as X12 and AS2 message handling.</span></span>

### <a name="protocol-pattern-templates"></a><span data-ttu-id="12a7d-116">Protokol düzeni şablonları</span><span class="sxs-lookup"><span data-stu-id="12a7d-116">Protocol pattern templates</span></span>
<span data-ttu-id="12a7d-117">İstek-yanıt gibi Protokolü düzenleri tümleştirmeler yanı sıra HTTP FTP ve SFTP arasında içeren mantıksal uygulamalar, bu şablonları oluşur.</span><span class="sxs-lookup"><span data-stu-id="12a7d-117">These templates consist of logic apps that contain protocol patterns such as request-response over HTTP as well as integrations across FTP and SFTP.</span></span> <span data-ttu-id="12a7d-118">Bunlar oldukları gibi veya temel olarak daha karmaşık Protokolü desenleri oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="12a7d-118">Use these as they exist, or as a basis for creating more complex protocol patterns.</span></span>  

### <a name="personal-productivity-templates"></a><span data-ttu-id="12a7d-119">Kişisel üretkenlik şablonları</span><span class="sxs-lookup"><span data-stu-id="12a7d-119">Personal productivity templates</span></span>
<span data-ttu-id="12a7d-120">Kişisel üretkenlik geliştirmeye yardımcı olmak için desenleri günlük anımsatıcıları ayarlamak, önemli iş öğeleri Yapılacaklar listelerine kapatma ve tek bir kullanıcı onayı adım kadar uzun görevleri otomatikleştirmek şablonları içerir.</span><span class="sxs-lookup"><span data-stu-id="12a7d-120">Patterns to help improve personal productivity include templates that set daily reminders, turn important work items into to-do lists, and automate lengthy tasks down to a single user approval step.</span></span>

### <a name="consumer-cloud-templates"></a><span data-ttu-id="12a7d-121">Tüketici bulut şablonları</span><span class="sxs-lookup"><span data-stu-id="12a7d-121">Consumer cloud templates</span></span>
<span data-ttu-id="12a7d-122">Twitter, boşluk ve e-posta, sosyal medya girişimleri pazarlama güçlendirme sonuçta özellikli gibi sosyal medya Hizmetleri ile tümleştirme basit şablonları.</span><span class="sxs-lookup"><span data-stu-id="12a7d-122">Simple templates that integrate with social media services such as Twitter, Slack, and email, ultimately capable of strengthening social media marketing initiatives.</span></span> <span data-ttu-id="12a7d-123">Bu da üretkenliklerini geleneksel yinelenen görevler üzerinde harcanan süre kaydederek yardımcı olabilecek cloudy kopyalama gibi şablonları içerir.</span><span class="sxs-lookup"><span data-stu-id="12a7d-123">These also include templates such as cloudy copying, which can help increase productivity by saving time spent on traditionally repetitive tasks.</span></span> 

## <a name="how-to-create-a-logic-app-using-a-template"></a><span data-ttu-id="12a7d-124">Bir şablonu kullanarak bir mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="12a7d-124">How to create a logic app using a template</span></span>
<span data-ttu-id="12a7d-125">Bir mantıksal uygulama şablonu kullanmaya başlamak için mantığı Uygulama Tasarımcısı'na gidin.</span><span class="sxs-lookup"><span data-stu-id="12a7d-125">To get started using a logic app template, go into the logic app designer.</span></span> <span data-ttu-id="12a7d-126">Varolan bir mantıksal uygulama açarak Tasarımcı girdiğinizden yoksa, mantıksal Uygulama Tasarımcısı görünümünüzde otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="12a7d-126">If you're entering the designer by opening an existing logic app, the logic app automatically loads in your designer view.</span></span> <span data-ttu-id="12a7d-127">Ancak, yeni bir mantıksal uygulama oluşturuyorsanız, aşağıdaki ekran görüntüsüne bakın.</span><span class="sxs-lookup"><span data-stu-id="12a7d-127">However, if you're creating a new logic app, you see the screen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

<span data-ttu-id="12a7d-128">Bu ekranda ya da boş mantıksal uygulama ya da önceden derlenmiş şablon ile başlatmak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12a7d-128">From this screen, you can either choose to start with a blank logic app or a pre-built template.</span></span> <span data-ttu-id="12a7d-129">Şablonlardan birini seçerseniz, ek bilgiler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="12a7d-129">If you select one of the templates, you are provided with additional information.</span></span> <span data-ttu-id="12a7d-130">Bu örnekte, kullandığımız *yeni bir dosya Dropbox'oluşturulduğunda, OneDrive kopyalama* şablonu.</span><span class="sxs-lookup"><span data-stu-id="12a7d-130">In this example, we use the *When a new file is created in Dropbox, copy it to OneDrive* template.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

<span data-ttu-id="12a7d-131">Şablon kullanmayı seçerseniz, yalnızca seçin *bu şablonu kullanmak* düğmesi.</span><span class="sxs-lookup"><span data-stu-id="12a7d-131">If you choose to use the template, just select the *use this template* button.</span></span> <span data-ttu-id="12a7d-132">Tabanlı hesaplarınız oturum açmak için şablonu hangi bağlayıcıların yararlanan istenir.</span><span class="sxs-lookup"><span data-stu-id="12a7d-132">You'll be asked to sign in to your accounts based on which connectors the template utilizes.</span></span> <span data-ttu-id="12a7d-133">Ya da daha önce bu bağlayıcıların bağlantıyla belirlediğinize göre seçebileceğiniz aşağıda görüldüğü gibi devam eder.</span><span class="sxs-lookup"><span data-stu-id="12a7d-133">Or, if you've previously established a connection with these connectors, you can select continue as seen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

<span data-ttu-id="12a7d-134">Bağlantı oluşturma ve seçtikten sonra *devam*, mantıksal Uygulama Tasarımcısı görünümünde açılır.</span><span class="sxs-lookup"><span data-stu-id="12a7d-134">After establishing the connection and selecting *continue*, the logic app opens in designer view.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

<span data-ttu-id="12a7d-135">Birçok şablonlarıyla olduğu gibi yukarıdaki örnekte, bazı zorunlu özellik alanları bağlayıcılar içinde doldurulması; Ancak, bazı hala bir değer doğru mantıksal uygulama dağıtmak için gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="12a7d-135">In the example above, as is the case with many templates, some of the mandatory property fields may be filled out within the connectors; however, some might still require a value before being able to properly deploy the logic app.</span></span> <span data-ttu-id="12a7d-136">Eksik alanların bazılarını girmeden dağıtmayı deneyin, hata iletisi ile bildirilir.</span><span class="sxs-lookup"><span data-stu-id="12a7d-136">If you try to deploy without entering some of the missing fields, you'll be notified with an error message.</span></span>

<span data-ttu-id="12a7d-137">Şablon Görüntüleyicisi dönmek istiyorsanız seçin *şablonları* üst gezinti çubuğu düğmesini.</span><span class="sxs-lookup"><span data-stu-id="12a7d-137">If you wish to return to the template viewer, select the *Templates* button in the top navigation bar.</span></span> <span data-ttu-id="12a7d-138">Şablon Görüntüleyicisi geçerek, kaydedilmemiş ilerleme kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="12a7d-138">By switching back to the template viewer, you lose any unsaved progress.</span></span> <span data-ttu-id="12a7d-139">Şablon Görüntüleyicisi'ne geçiş öncesinde bu bildiren bir uyarı iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="12a7d-139">Prior to switching back into template viewer, you'll see a warning message notifying you of this.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-to-deploy-a-logic-app-created-from-a-template"></a><span data-ttu-id="12a7d-140">Şablondan oluşturulan bir mantıksal uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="12a7d-140">How to deploy a logic app created from a template</span></span>
<span data-ttu-id="12a7d-141">Şablonunuzu yüklü ve istediğiniz tüm değişiklikleri yapılan sonra Kaydet seçeneğini sol üst köşedeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="12a7d-141">Once you have loaded your template and made any desired changes, select the save button in the upper left corner.</span></span> <span data-ttu-id="12a7d-142">Bu kaydeder ve mantıksal uygulamanızı yayımlar.</span><span class="sxs-lookup"><span data-stu-id="12a7d-142">This saves and publishes your logic app.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

<span data-ttu-id="12a7d-143">Daha fazla adım var olan bir mantıksal uygulama şablonu içine ekleyin veya genel düzenlemeler hakkında daha fazla bilgi isterseniz, hakkında daha fazla okuma [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="12a7d-143">If you would like more information on how to add more steps into an existing logic app template, or make edits in general, read more at [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

