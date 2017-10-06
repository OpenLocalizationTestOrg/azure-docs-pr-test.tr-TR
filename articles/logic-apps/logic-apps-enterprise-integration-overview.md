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
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a>Genel Bakış: B2B senaryolarını ve hello Kurumsal tümleştirme paketi ile iletişim

İşletmeden işletmeye (B2B) iş akışları ve Azure Logic Apps ile sorunsuz iletişimi için Kurumsal tümleştirme senaryolarına Microsoft'un bulut tabanlı çözümü, hello Kurumsal tümleştirme paketi ile etkinleştirebilirsiniz. Farklı protokollere ve biçimleri kullandıkları olsa bile kuruluşlar iletileri elektronik olarak değiştirebilir. Merhaba paketi farklı biçimlerde kurumların sistemleri yorumlanacağı ve işlem bir biçime dönüştürür. Kuruluşların dahil, endüstri standardı protokoller üzerinden ileti alışverişi [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), ve [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md). Ayrıca, şifreleme ve dijital imzalar iletilerle güvenliğini sağlayabilirsiniz.

BizTalk Server veya Microsoft Azure BizTalk Services ile bilginiz varsa, çoğu kavramları benzer olduğundan hello Kurumsal tümleştirme kolay toouse özellikleridir. Temel farklardan biri Kurumsal tümleştirme tümleştirme hesapları toosimplify hello depolama ve yönetim B2B iletişimde kullanılan yapılarının kullanmasıdır. 

Mimari, Enterprise Integration Pack Merhaba "tümleştirme hesapları" temel alınır. Bu hesapları şemaları, iş ortakları, sertifikaları, maps ve anlaşmaları gibi tüm, yapıları, depolama, bulut tabanlı kapsayıcı görevi görür. Bu yapıları toodesign kullanın, dağıtmak ve B2B uygulamalarınızı ve ayrıca mantıksal uygulamalar için toobuild B2B iş akışlarını korumak. Ancak bu yapıtların kullanmadan önce tümleştirme hesap tooyour mantıksal uygulamanızı öncelikle bağlamanız gerekir. Bundan sonra mantıksal uygulamanızı tümleştirme hesabınızın yapılarına erişebilir.

## <a name="why-should-you-use-enterprise-integration"></a>Neden Kurumsal tümleştirme kullanmalısınız?

* Kurumsal tümleştirme ile tek bir yerde--tümleştirme hesabınızı tüm yapıtları depolayabilirsiniz.
* B2B iş akışları oluşturmak ve hello Azure Logic Apps altyapısı ve tüm bağlayıcılar kullanarak üçüncü taraf hizmet olarak yazılım (SaaS) uygulamaları, şirket içi uygulamalar ve özel uygulamalar ile tümleştirebilirsiniz.
* Logic apps ile Azure işlevleri için özel kod oluşturabilirsiniz.

## <a name="how-tooget-started-with-enterprise-integration"></a>Tooget Kurumsal tümleştirme ile çalışmaya nasıl?

Derleme ve hello Enterprise Integration Pack Merhaba hello mantığı Uygulama Tasarımcısı aracılığıyla B2B uygulamalarla yönetmek **Azure portal**. Logic apps ile yönetebilmeniz için [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell konularına").

Hello Azure portal uygulamaları oluşturabilmeniz için önce gerçekleştirmeniz gereken hello üst düzey adımlar şunlardır:

![Genel Bakış görüntüsü](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a>Bazı genel senaryolar nelerdir?

Kurumsal tümleştirme bu endüstri standartları destekler:

* EDI - elektronik veri değişimi
* EAI - Kurumsal uygulama tümleştirmesi

## <a name="heres-what-you-need-tooget-started"></a>İşte başlatılan tooget gerekir

* Bir Azure aboneliği bir tümleştirme Hesapla
* Visual Studio 2015 toocreate eşlemeleri ve şemaları
* [Visual Studio 2015 2.0 için Microsoft Azure Logic Apps Enterprise tümleştirme araçları](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a>Hemen deneyin

[Tam olarak işlevsel örnek AS2 gönderme dağıtma ve mantıksal uygulama alma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) Azure Logic Apps için hello B2B özelliklerini kullanır.

## <a name="learn-more"></a>Daha fazla bilgi edinin
* [Anlaşmaları](../logic-apps/logic-apps-enterprise-integration-agreements.md "Kurumsal tümleştirme anlaşmaları hakkında bilgi edinin")
* [İş tooBusiness (B2B) senaryolarını](../logic-apps/logic-apps-enterprise-integration-b2b.md "öğrenin nasıl toocreate Logic apps ile B2B özellikleri")  
* [Sertifikaları](logic-apps-enterprise-integration-certificates.md "kuruluş tümleştirme sertifikaları hakkında bilgi edinin")
* [Düz dosya kodlama/kod çözme](logic-apps-enterprise-integration-flatfile.md "öğrenin nasıl tooencode ve düz dosya içeriğini kod çözme")  
* [Tümleştirme hesapları](../logic-apps/logic-apps-enterprise-integration-accounts.md "tümleştirme hesapları hakkında daha fazla bilgi edinin")
* [Eşlemeleri](../logic-apps/logic-apps-enterprise-integration-maps.md "Kurumsal tümleştirme eşlemeleri hakkında bilgi edinin")
* [İş ortakları](logic-apps-enterprise-integration-partners.md "Kurumsal tümleştirme ortakları hakkında bilgi edinin")
* [Şemalar](logic-apps-enterprise-integration-schemas.md "Kurumsal tümleştirme şemaları hakkında bilgi edinin")
* [XML ileti doğrulama](logic-apps-enterprise-integration-xml.md "Logic apps ile nasıl toovalidate XML iletileri öğrenin")
* [XML dönüştürme](logic-apps-enterprise-integration-transform.md "Kurumsal tümleştirme eşlemeleri hakkında bilgi edinin")
* [Enterprise Integration bağlayıcıları](../connectors/apis-list.md "enterprise Integration pack bağlayıcıları hakkında bilgi edinin")
* [Tümleştirme hesap meta veri](../logic-apps/logic-apps-enterprise-integration-metadata.md "tümleştirme hesap meta veriler hakkında bilgi edinin")
* [B2B iletileri izlemeniz](logic-apps-monitor-b2b-message.md "B2B iletileri izleme hakkında daha fazla bilgi edinin")
* [B2B iletileri OMS portalında izleme](logic-apps-track-b2b-messages-omsportal.md "B2B iletileri OMS portalında izleme hakkında daha fazla bilgi edinin")

