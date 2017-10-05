---
title: "Azure App Service Web uygulaması Linux'ta Ruby kullanarak | Microsoft Docs"
description: "Azure App Service Web uygulaması Linux'ta Ruby kullanarak."
keywords: "Azure uygulama hizmeti, web uygulaması, SSS, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a>Ruby Linux üzerinde Web uygulamasında kullanma #

Bizim arka uç için en son güncelleştirme ile Söyleniş v.2.3 desteği sunmuştur. Linux web uygulamanızın yapılandırma ayarlayarak, uygulama yığınını değiştirebilirsiniz.

## <a name="using-the-azure-portal"></a>Azure portalını kullanma ##

Yeni menüsünden [Azure portal](https://portal.azure.com), aşağıdaki görüntüde gösterildiği gibi Web + Mobil Seçenek'dan Linux üzerinde bir Web uygulaması oluşturmayı seçebilirsiniz:

![Azure portalında bir web uygulaması oluşturmaya başla][1]

Ardından, **Oluştur dikey** aşağıdaki görüntüde gösterildiği gibi açılır:

![Oluşturma dikey penceresi][2]

1. Web uygulamanızı bir ad verin.
2. Varolan bir kaynak grubu seçin veya yeni bir tane oluşturun. (Kullanılabilir bölgelerde bkz [sınırlamalar bölüm](app-service-linux-intro.md).)
3. Var olan bir Azure uygulama hizmeti planı seçin veya yeni bir tane oluşturun. (Uygulama hizmeti planı notlara bakın [sınırlamalar bölüm](app-service-linux-intro.md).)
4. Söyleniş yerleşik çalışma zamanı yığınlar seçin.

Söyleniş web uygulamanızı oluşturulan sonra Git veya FTP kullanarak dağıtabilirsiniz.

Söyleniş uygulama oluşturma hakkında daha fazla bilgi edinmek için [get Başlarken Kılavuzu](app-service-linux-ruby-get-started.md)

## <a name="next-steps"></a>Sonraki adımlar
* [Linux üzerinde Web uygulaması nedir?](app-service-linux-intro.md)
* [Azure App Service için Yerel Git Dağıtımı](app-service-deploy-local-git.md)
* [Azure App Service Web uygulaması Linux SSS](app-service-linux-faq.md)
* [Linux üzerinde Azure Web uygulaması ile Söyleniş bir uygulama oluşturun.](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png