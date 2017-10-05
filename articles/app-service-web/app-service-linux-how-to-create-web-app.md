---
title: "Linux üzerinde çalışan bir Azure web uygulaması oluşturma | Microsoft Docs"
description: "Web uygulaması oluşturma için iş akışı Linux Azure Web uygulaması."
keywords: "Azure uygulama hizmeti, web uygulaması, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Linux üzerinde çalışan bir Azure web uygulaması oluşturma

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a>Web uygulamanızı oluşturmak için Azure portalını kullanma
Web uygulamanız Linux'ta oluşturmaya başlamadan [Azure portal](https://portal.azure.com) aşağıdaki görüntüde gösterildiği gibi:

![Azure portalında bir web uygulaması oluşturmaya başla][1]

Ardından, **Oluştur dikey** aşağıdaki görüntüde gösterildiği gibi açılır:

![Oluşturma dikey penceresi][2]

1. Web uygulamanızı bir ad verin.
2. Varolan bir kaynak grubu seçin veya yeni bir tane oluşturun. (Kullanılabilir bölgelerde bkz [sınırlamalar bölüm](app-service-linux-intro.md).)
3. Var olan bir Azure uygulama hizmeti planı seçin veya yeni bir tane oluşturun. (Uygulama hizmeti planı notlara bakın [sınırlamalar bölüm](app-service-linux-intro.md).)
4. Kullanmak istediğiniz uygulama yığını seçin. Node.js, PHP, .net birkaç sürümleri arasında seçim yapabilirsiniz çekirdek ve Ruby.

Uygulamayı oluşturduktan sonra uygulama yığın uygulama ayarlarından aşağıdaki görüntüde gösterildiği gibi değiştirebilirsiniz:

![Uygulama ayarları][3]

## <a name="deploy-your-web-app"></a>Web uygulamanızı dağıtın
Seçme **dağıtım seçenekleri** yönetimden portal size uygulamanızı dağıtmak için yerel Git veya GitHub deposunu kullanmak üzere seçeneği sunar. Kalan yönergeleri Linux olmayan web uygulaması için benzer. ' Ndaki yönergeleri izleyin [yerel Git dağıtımı](app-service-deploy-local-git.md) veya [sürekli dağıtım](app-service-continuous-deployment.md) uygulamanızı dağıtmak için.

FTP, uygulamanızın Web sitenize yüklemek için de kullanabilirsiniz. Aşağıdaki görüntüde gösterildiği gibi tanılama günlüklerini bölümünden web uygulamanız için FTP uç noktasını alın:

![Tanılama günlükleri][4]

## <a name="next-steps"></a>Sonraki adımlar
* [Linux üzerinde Azure Web uygulaması nedir?](app-service-linux-intro.md)
* [Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak](app-service-linux-using-nodejs-pm2.md)
* [Azure App Service Web uygulaması Linux'ta Ruby kullanma](app-service-linux-ruby-get-started.md)
* [Azure App Service Web uygulaması Linux SSS](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
