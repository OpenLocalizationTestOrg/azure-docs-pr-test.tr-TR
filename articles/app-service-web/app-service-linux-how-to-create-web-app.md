---
title: "aaaCreate bir Azure web uygulaması Linux üzerinde çalışan | Microsoft Docs"
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
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Linux üzerinde çalışan bir Azure web uygulaması oluşturma

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a>Web uygulamanızı Hello Azure portal toocreate kullanın
Web uygulamanız hello Linux'ta oluşturma başlatabilirsiniz [Azure portal](https://portal.azure.com) hello görüntü aşağıdaki gösterildiği gibi:

![Azure portal hello üzerinde bir web uygulaması oluşturmaya başla][1]

Ardından, hello **Oluştur dikey** hello görüntü aşağıdaki gösterildiği gibi açılır:

![Merhaba Oluştur dikey penceresi][2]

1. Web uygulamanızı bir ad verin.
2. Varolan bir kaynak grubu seçin veya yeni bir tane oluşturun. (Merhaba kullanılabilir bölgelerde bkz [sınırlamalar bölüm](app-service-linux-intro.md).)
3. Var olan bir Azure uygulama hizmeti planı seçin veya yeni bir tane oluşturun. (Uygulama hizmeti planı notları hello bkz [sınırlamalar bölüm](app-service-linux-intro.md).)
4. Merhaba uygulamasını seçin toouse düşündüğünüz yığını. Node.js, PHP, .net birkaç sürümleri arasında seçim yapabilirsiniz çekirdek ve Ruby.

Merhaba uygulama oluşturduktan sonra hello uygulama yığınını hello uygulama ayarlarından hello görüntü aşağıdaki gösterildiği gibi değiştirebilirsiniz:

![Uygulama ayarları][3]

## <a name="deploy-your-web-app"></a>Web uygulamanızı dağıtın
Seçme **dağıtım seçenekleri** hello Yönetim Portalı sağlar, uygulamanızın seçeneği toouse yerel Git veya GitHub depo toodeploy hello. bir Linux olmayan web uygulaması için benzer toothose hello yönergeleri Hello kalan var. Merhaba yönergeleri takip edebilirsiniz [yerel Git dağıtımı](app-service-deploy-local-git.md) veya [sürekli dağıtım](app-service-continuous-deployment.md) toodeploy uygulamanızı.

Uygulama tooyour sitenizi FTP tooupload de kullanabilirsiniz. Merhaba FTP endpoint web uygulamanız için hello tanılama logs bölümü hello görüntü aşağıdaki gösterildiği gibi alabilirsiniz:

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
