---
title: "B2B - Azure mantıksal uygulamaları için Kurumsal tümleştirme | Microsoft Docs"
description: "B2B iş akışları oluşturmak ve logic apps Enterprise tümleştirme paketi ile Kurumsal tümleştirme senaryolarına desteği"
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
ms.openlocfilehash: 9462707db03ecfcc3d5186ce7ded8655ad3bdcc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-the-enterprise-integration-pack"></a><span data-ttu-id="618dc-103">Genel Bakış: B2B senaryolarını ve kurumsal tümleştirme paketi ile iletişim</span><span class="sxs-lookup"><span data-stu-id="618dc-103">Overview: B2B scenarios and communication with the Enterprise Integration Pack</span></span>

<span data-ttu-id="618dc-104">İşletmeden işletmeye (B2B) iş akışları ve Azure Logic Apps ile sorunsuz iletişimi için Kurumsal tümleştirme senaryolarına Microsoft'un bulut tabanlı çözümü, Kurumsal tümleştirme paketi ile etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="618dc-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, the Enterprise Integration Pack.</span></span> <span data-ttu-id="618dc-105">Farklı protokollere ve biçimleri kullandıkları olsa bile kuruluşlar iletileri elektronik olarak değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="618dc-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="618dc-106">Paketi farklı biçimlerde kurumların sistemleri yorumlanacağı ve işlem bir biçime dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="618dc-106">The pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="618dc-107">Kuruluşların dahil, endüstri standardı protokoller üzerinden ileti alışverişi [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), ve [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="618dc-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="618dc-108">Ayrıca, şifreleme ve dijital imzalar iletilerle güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="618dc-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="618dc-109">BizTalk Server veya Microsoft Azure BizTalk Services ile bilginiz varsa, çoğu kavramları benzer olduğundan, Kurumsal tümleştirme özelliklerine kullanımı kolay.</span><span class="sxs-lookup"><span data-stu-id="618dc-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, the Enterprise Integration features are easy to use because most concepts are similar.</span></span> <span data-ttu-id="618dc-110">Temel farklardan biri Kurumsal tümleştirme tümleştirme hesapları depolama ve B2B iletişimde kullanılan yapılarının yönetimini basitleştirmek için kullanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="618dc-110">One major difference is that Enterprise Integration uses integration accounts to simplify the storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="618dc-111">Mimari, Kurumsal tümleştirme paketi "tümleştirme hesapları" temel alınır.</span><span class="sxs-lookup"><span data-stu-id="618dc-111">Architecturally, the Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="618dc-112">Bu hesapları şemaları, iş ortakları, sertifikaları, maps ve anlaşmaları gibi tüm, yapıları, depolama, bulut tabanlı kapsayıcı görevi görür.</span><span class="sxs-lookup"><span data-stu-id="618dc-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="618dc-113">Bu yapıtların tasarlamak, dağıtmak ve B2B uygulamalarınızı korumak için ve ayrıca logic apps B2B iş akışları oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="618dc-113">You can use these artifacts to design, deploy, and maintain your B2B apps and also to build B2B workflows for logic apps.</span></span> <span data-ttu-id="618dc-114">Ancak bu yapıtların kullanmadan önce mantıksal uygulamanızı tümleştirme hesabınızı bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="618dc-114">But before you can use these artifacts, you must first link your integration account to your logic app.</span></span> <span data-ttu-id="618dc-115">Bundan sonra mantıksal uygulamanızı tümleştirme hesabınızın yapılarına erişebilir.</span><span class="sxs-lookup"><span data-stu-id="618dc-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="618dc-116">Neden Kurumsal tümleştirme kullanmalısınız?</span><span class="sxs-lookup"><span data-stu-id="618dc-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="618dc-117">Kurumsal tümleştirme ile tek bir yerde--tümleştirme hesabınızı tüm yapıtları depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="618dc-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="618dc-118">B2B iş akışları oluşturmak ve Azure Logic Apps altyapısı ve tüm bağlayıcılar kullanarak üçüncü taraf hizmet olarak yazılım (SaaS) uygulamaları, şirket içi uygulamalar ve özel uygulamalar ile tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="618dc-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using the Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="618dc-119">Logic apps ile Azure işlevleri için özel kod oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="618dc-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-to-get-started-with-enterprise-integration"></a><span data-ttu-id="618dc-120">Kurumsal tümleştirme ile çalışmaya başlamak nasıl?</span><span class="sxs-lookup"><span data-stu-id="618dc-120">How to get started with enterprise integration?</span></span>

<span data-ttu-id="618dc-121">Derleme ve Enterprise Integration Pack mantığı Uygulama Tasarımcısı'nda aracılığıyla B2B uygulamalarla yönetmek **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="618dc-121">You can build and manage B2B apps with the Enterprise Integration Pack through the Logic App Designer in the **Azure portal**.</span></span> <span data-ttu-id="618dc-122">Logic apps ile yönetebilmeniz için [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell konularına").</span><span class="sxs-lookup"><span data-stu-id="618dc-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="618dc-123">Azure portalında uygulamaları oluşturabilmeniz için önce gerçekleştirmeniz gereken üst düzey adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="618dc-123">Here are the high-level steps you must take before you can create apps in the Azure portal:</span></span>

![Genel Bakış görüntüsü](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="618dc-125">Bazı genel senaryolar nelerdir?</span><span class="sxs-lookup"><span data-stu-id="618dc-125">What are some common scenarios?</span></span>

<span data-ttu-id="618dc-126">Kurumsal tümleştirme bu endüstri standartları destekler:</span><span class="sxs-lookup"><span data-stu-id="618dc-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="618dc-127">EDI - elektronik veri değişimi</span><span class="sxs-lookup"><span data-stu-id="618dc-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="618dc-128">EAI - Kurumsal uygulama tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="618dc-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-to-get-started"></a><span data-ttu-id="618dc-129">İşte başlamak için ihtiyacınız olanlar</span><span class="sxs-lookup"><span data-stu-id="618dc-129">Here's what you need to get started</span></span>

* <span data-ttu-id="618dc-130">Bir Azure aboneliği bir tümleştirme Hesapla</span><span class="sxs-lookup"><span data-stu-id="618dc-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="618dc-131">Maps ve şemaları oluşturmak için Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="618dc-131">Visual Studio 2015 to create maps and schemas</span></span>
* [<span data-ttu-id="618dc-132">Visual Studio 2015 2.0 için Microsoft Azure Logic Apps Enterprise tümleştirme araçları</span><span class="sxs-lookup"><span data-stu-id="618dc-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="618dc-133">Hemen deneyin</span><span class="sxs-lookup"><span data-stu-id="618dc-133">Try it now</span></span>

<span data-ttu-id="618dc-134">[Tam olarak işlevsel örnek AS2 gönderme dağıtma ve mantıksal uygulama alma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) , B2B özelliklerini Azure Logic Apps için kullanır.</span><span class="sxs-lookup"><span data-stu-id="618dc-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses the B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="618dc-135">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="618dc-135">Learn more</span></span>
* [<span data-ttu-id="618dc-136">Anlaşmaları</span><span class="sxs-lookup"><span data-stu-id="618dc-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")
* [<span data-ttu-id="618dc-137">İşletmeler için (B2B) senaryolarını</span><span class="sxs-lookup"><span data-stu-id="618dc-137">Business to Business (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "B2B özelliklerle mantıksal uygulamaları oluşturmayı öğrenin")  
* [<span data-ttu-id="618dc-138">Sertifikaları</span><span class="sxs-lookup"><span data-stu-id="618dc-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "kuruluş tümleştirme sertifikaları hakkında bilgi edinin")
* [<span data-ttu-id="618dc-139">Düz dosya kodlama/kod çözme</span><span class="sxs-lookup"><span data-stu-id="618dc-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "kodlamak ve düz dosya içeriğini kod çözme hakkında bilgi edinin")  
* [<span data-ttu-id="618dc-140">Tümleştirme hesapları</span><span class="sxs-lookup"><span data-stu-id="618dc-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "tümleştirme hesapları hakkında daha fazla bilgi edinin")
* [<span data-ttu-id="618dc-141">Eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="618dc-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Kurumsal tümleştirme eşlemeleri hakkında bilgi edinin")
* [<span data-ttu-id="618dc-142">İş ortakları</span><span class="sxs-lookup"><span data-stu-id="618dc-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Kurumsal tümleştirme ortakları hakkında bilgi edinin")
* [<span data-ttu-id="618dc-143">Şemalar</span><span class="sxs-lookup"><span data-stu-id="618dc-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Kurumsal tümleştirme şemaları hakkında bilgi edinin")
* [<span data-ttu-id="618dc-144">XML ileti doğrulama</span><span class="sxs-lookup"><span data-stu-id="618dc-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "XML iletileri Logic apps ile doğrulama öğrenin")
* [<span data-ttu-id="618dc-145">XML dönüştürme</span><span class="sxs-lookup"><span data-stu-id="618dc-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Kurumsal tümleştirme eşlemeleri hakkında bilgi edinin")
* [<span data-ttu-id="618dc-146">Enterprise Integration bağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="618dc-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "enterprise Integration pack bağlayıcıları hakkında bilgi edinin")
* [<span data-ttu-id="618dc-147">Tümleştirme hesap meta veri</span><span class="sxs-lookup"><span data-stu-id="618dc-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "tümleştirme hesap meta veriler hakkında bilgi edinin")
* [<span data-ttu-id="618dc-148">B2B iletileri izlemeniz</span><span class="sxs-lookup"><span data-stu-id="618dc-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "B2B iletileri izleme hakkında daha fazla bilgi edinin")
* [<span data-ttu-id="618dc-149">B2B iletileri OMS portalında izleme</span><span class="sxs-lookup"><span data-stu-id="618dc-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "B2B iletileri OMS portalında izleme hakkında daha fazla bilgi edinin")

