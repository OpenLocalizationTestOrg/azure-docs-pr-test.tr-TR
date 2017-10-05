---
title: "Uzantılar uygulama - Azure AD B2C | Microsoft Docs"
description: "B2c uzantıları uygulama geri yükleme"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: 17500b572a0e92c1c233c6967840a5b6d96e21cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-extensions-app"></a>Azure AD B2C: Uzantıları uygulaması

Azure AD B2C dizini oluşturulduğunda, bir uygulama olarak adlandırılan `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` yeni dizini içinde otomatik olarak oluşturulur. Bu uygulamayı denir **b2c uzantıları uygulaması**, görünür olan *uygulama kayıtlar*. Azure AD B2C hizmeti tarafından kullanıcılar ve özel öznitelikler hakkında bilgi depolamak için kullanılır. Uygulama silinirse, Azure AD B2C düzgün çalışmaz ve üretim ortamınıza etkilenecek.

> [!IMPORTANT]
> Kiracı hemen silinecek planlama sürece b2c uzantıları uygulama silmeyin. Uygulama 30 günden fazla bir süre için silinen kalırsa, kullanıcı bilgilerini kalıcı olarak kaybolur.

## <a name="verifying-that-the-extensions-app-is-present"></a>Uzantılar uygulama mevcut olduğunu doğrulama

B2c uzantıları uygulama mevcut olduğunu doğrulamak için:

1. Azure AD B2C kiracınızın içinde tıklayın **daha fazla hizmet** sol taraftaki gezinti menüsünde.
1. Aramak ve açmak **uygulama kayıtlar**.
1. İle başlayan uygulama Ara **b2c uzantıları uygulaması**

## <a name="recover-the-extensions-app"></a>Uzantılar uygulama Kurtar

B2c uzantıları uygulama yanlışlıkla sildiyseniz, kurtarma için 30 gün sahip. Grafik API'sini kullanarak uygulamayı geri yükleyebilirsiniz:

1. Gözat [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).
1. Siteye silinen uygulama için geri yüklemek istediğiniz Azure AD B2C dizini için genel yönetici olarak oturum açın.
1. Bir HTTP GET URL karşı sorun `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` api-version ile 1.6 =. Değiştirdiğinizden emin olun `{tenantName}` Kiracı adınız ile. Bu işlem tüm son 30 gün içinde silinmiş uygulamaları listeler.
1. 'B2c uzantısı uygulama' ve kopyalama ile adı başladığı listesinde uygulamayı bulmak, `objectid` özellik değeri.
1. Bir HTTP POST URL karşı sorun `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`. Değiştir `{OBJECTID}` URL ile kısmı `objectid` önceki adımdan. 

Şimdi yapabilir olmalıdır [geri yüklenen uygulama görmek](#verifying-that-the-extensions-app-is-present) Azure portalında.

> [!NOTE]
> Son 30 gün içinde sildiyseniz uygulamanın yalnızca geri yüklenebilir. 30 günden fazla olması durumunda, verileri kalıcı olarak kaybolur. Daha fazla yardım için destek bileti dosya.