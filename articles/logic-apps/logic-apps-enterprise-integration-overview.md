---
title: "aaaEnterprise B2B - Azure Logic Apps için tümleştirme | Microsoft Docs"
description: "B2B iş akışları oluşturmak ve logic apps hello Kurumsal tümleştirme paketi ile Kurumsal tümleştirme senaryolarına desteği"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a><span data-ttu-id="6968b-103">Genel Bakış: B2B senaryolarını ve hello Kurumsal tümleştirme paketi ile iletişim</span><span class="sxs-lookup"><span data-stu-id="6968b-103">Overview: B2B scenarios and communication with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="6968b-104">İşletmeden işletmeye (B2B) iş akışları ve Azure Logic Apps ile sorunsuz iletişimi için Kurumsal tümleştirme senaryolarına Microsoft'un bulut tabanlı çözümü, hello Kurumsal tümleştirme paketi ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6968b-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, hello Enterprise Integration Pack.</span></span> <span data-ttu-id="6968b-105">Farklı protokollere ve biçimleri kullandıkları olsa bile kuruluşlar iletileri elektronik olarak değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="6968b-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="6968b-106">Merhaba paketi farklı biçimlerde kurumların sistemleri yorumlanacağı ve işlem bir biçime dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="6968b-106">hello pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="6968b-107">Kuruluşların dahil, endüstri standardı protokoller üzerinden ileti alışverişi [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), ve [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="6968b-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="6968b-108">Ayrıca, şifreleme ve dijital imzalar iletilerle güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6968b-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="6968b-109">BizTalk Server veya Microsoft Azure BizTalk Services ile bilginiz varsa, çoğu kavramları benzer olduğundan hello Kurumsal tümleştirme kolay toouse özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="6968b-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, hello Enterprise Integration features are easy toouse because most concepts are similar.</span></span> <span data-ttu-id="6968b-110">Temel farklardan biri Kurumsal tümleştirme tümleştirme hesapları toosimplify hello depolama ve yönetim B2B iletişimde kullanılan yapılarının kullanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="6968b-110">One major difference is that Enterprise Integration uses integration accounts toosimplify hello storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="6968b-111">Mimari, Enterprise Integration Pack Merhaba "tümleştirme hesapları" temel alınır.</span><span class="sxs-lookup"><span data-stu-id="6968b-111">Architecturally, hello Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="6968b-112">Bu hesapları şemaları, iş ortakları, sertifikaları, maps ve anlaşmaları gibi tüm, yapıları, depolama, bulut tabanlı kapsayıcı görevi görür.</span><span class="sxs-lookup"><span data-stu-id="6968b-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="6968b-113">Bu yapıları toodesign kullanın, dağıtmak ve B2B uygulamalarınızı ve ayrıca mantıksal uygulamalar için toobuild B2B iş akışlarını korumak.</span><span class="sxs-lookup"><span data-stu-id="6968b-113">You can use these artifacts toodesign, deploy, and maintain your B2B apps and also toobuild B2B workflows for logic apps.</span></span> <span data-ttu-id="6968b-114">Ancak bu yapıtların kullanmadan önce tümleştirme hesap tooyour mantıksal uygulamanızı öncelikle bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6968b-114">But before you can use these artifacts, you must first link your integration account tooyour logic app.</span></span> <span data-ttu-id="6968b-115">Bundan sonra mantıksal uygulamanızı tümleştirme hesabınızın yapılarına erişebilir.</span><span class="sxs-lookup"><span data-stu-id="6968b-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="6968b-116">Neden Kurumsal tümleştirme kullanmalısınız?</span><span class="sxs-lookup"><span data-stu-id="6968b-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="6968b-117">Kurumsal tümleştirme ile tek bir yerde--tümleştirme hesabınızı tüm yapıtları depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6968b-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="6968b-118">B2B iş akışları oluşturmak ve hello Azure Logic Apps altyapısı ve tüm bağlayıcılar kullanarak üçüncü taraf hizmet olarak yazılım (SaaS) uygulamaları, şirket içi uygulamalar ve özel uygulamalar ile tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6968b-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using hello Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="6968b-119">Logic apps ile Azure işlevleri için özel kod oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6968b-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-tooget-started-with-enterprise-integration"></a><span data-ttu-id="6968b-120">Tooget Kurumsal tümleştirme ile çalışmaya nasıl?</span><span class="sxs-lookup"><span data-stu-id="6968b-120">How tooget started with enterprise integration?</span></span>

<span data-ttu-id="6968b-121">Derleme ve hello Enterprise Integration Pack Merhaba hello mantığı Uygulama Tasarımcısı aracılığıyla B2B uygulamalarla yönetmek **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="6968b-121">You can build and manage B2B apps with hello Enterprise Integration Pack through hello Logic App Designer in hello **Azure portal**.</span></span> <span data-ttu-id="6968b-122">Logic apps ile yönetebilmeniz için [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell konularına").</span><span class="sxs-lookup"><span data-stu-id="6968b-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="6968b-123">Hello Azure portal uygulamaları oluşturabilmeniz için önce gerçekleştirmeniz gereken hello üst düzey adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6968b-123">Here are hello high-level steps you must take before you can create apps in hello Azure portal:</span></span>

![Genel Bakış görüntüsü](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="6968b-125">Bazı genel senaryolar nelerdir?</span><span class="sxs-lookup"><span data-stu-id="6968b-125">What are some common scenarios?</span></span>

<span data-ttu-id="6968b-126">Kurumsal tümleştirme bu endüstri standartları destekler:</span><span class="sxs-lookup"><span data-stu-id="6968b-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="6968b-127">EDI - elektronik veri değişimi</span><span class="sxs-lookup"><span data-stu-id="6968b-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="6968b-128">EAI - Kurumsal uygulama tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="6968b-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-tooget-started"></a><span data-ttu-id="6968b-129">İşte başlatılan tooget gerekir</span><span class="sxs-lookup"><span data-stu-id="6968b-129">Here's what you need tooget started</span></span>

* <span data-ttu-id="6968b-130">Bir Azure aboneliği bir tümleştirme Hesapla</span><span class="sxs-lookup"><span data-stu-id="6968b-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="6968b-131">Visual Studio 2015 toocreate eşlemeleri ve şemaları</span><span class="sxs-lookup"><span data-stu-id="6968b-131">Visual Studio 2015 toocreate maps and schemas</span></span>
* [<span data-ttu-id="6968b-132">Visual Studio 2015 2.0 için Microsoft Azure Logic Apps Enterprise tümleştirme araçları</span><span class="sxs-lookup"><span data-stu-id="6968b-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="6968b-133">Hemen deneyin</span><span class="sxs-lookup"><span data-stu-id="6968b-133">Try it now</span></span>

<span data-ttu-id="6968b-134">[Tam olarak işlevsel örnek AS2 gönderme dağıtma ve mantıksal uygulama alma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) Azure Logic Apps için hello B2B özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6968b-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses hello B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="6968b-135">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="6968b-135">Learn more</span></span>
* [<span data-ttu-id="6968b-136">Anlaşmaları</span><span class="sxs-lookup"><span data-stu-id="6968b-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")
* [<span data-ttu-id="6968b-137">İş tooBusiness (B2B) senaryolarını</span><span class="sxs-lookup"><span data-stu-id="6968b-137">Business tooBusiness (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "öğrenin nasıl toocreate Logic apps ile B2B özellikleri")  
* [<span data-ttu-id="6968b-138">Sertifikaları</span><span class="sxs-lookup"><span data-stu-id="6968b-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "kuruluş tümleştirme sertifikaları hakkında bilgi edinin")
* [<span data-ttu-id="6968b-139">Düz dosya kodlama/kod çözme</span><span class="sxs-lookup"><span data-stu-id="6968b-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "öğrenin nasıl tooencode ve düz dosya içeriğini kod çözme")  
* [<span data-ttu-id="6968b-140">Tümleştirme hesapları</span><span class="sxs-lookup"><span data-stu-id="6968b-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "tümleştirme hesapları hakkında daha fazla bilgi edinin")
* [<span data-ttu-id="6968b-141">Eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="6968b-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Kurumsal tümleştirme eşlemeleri hakkında bilgi edinin")
* [<span data-ttu-id="6968b-142">İş ortakları</span><span class="sxs-lookup"><span data-stu-id="6968b-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Kurumsal tümleştirme ortakları hakkında bilgi edinin")
* [<span data-ttu-id="6968b-143">Şemalar</span><span class="sxs-lookup"><span data-stu-id="6968b-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Kurumsal tümleştirme şemaları hakkında bilgi edinin")
* [<span data-ttu-id="6968b-144">XML ileti doğrulama</span><span class="sxs-lookup"><span data-stu-id="6968b-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "Logic apps ile nasıl toovalidate XML iletileri öğrenin")
* [<span data-ttu-id="6968b-145">XML dönüştürme</span><span class="sxs-lookup"><span data-stu-id="6968b-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Kurumsal tümleştirme eşlemeleri hakkında bilgi edinin")
* [<span data-ttu-id="6968b-146">Enterprise Integration bağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="6968b-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "enterprise Integration pack bağlayıcıları hakkında bilgi edinin")
* [<span data-ttu-id="6968b-147">Tümleştirme hesap meta veri</span><span class="sxs-lookup"><span data-stu-id="6968b-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "tümleştirme hesap meta veriler hakkında bilgi edinin")
* [<span data-ttu-id="6968b-148">B2B iletileri izlemeniz</span><span class="sxs-lookup"><span data-stu-id="6968b-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "B2B iletileri izleme hakkında daha fazla bilgi edinin")
* [<span data-ttu-id="6968b-149">B2B iletileri OMS portalında izleme</span><span class="sxs-lookup"><span data-stu-id="6968b-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "B2B iletileri OMS portalında izleme hakkında daha fazla bilgi edinin")

