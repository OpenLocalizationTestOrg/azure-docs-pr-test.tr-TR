---
title: "Uzantılar uygulama - Azure AD B2C | Microsoft Docs"
description: "Merhaba b2c uzantıları uygulama geri yükleme"
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
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a>Azure AD B2C: Uzantıları uygulaması

Azure AD B2C dizini oluşturulduğunda, bir uygulama olarak adlandırılan `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` hello yeni dizini içinde otomatik olarak oluşturulur. Bu uygulama, başvurulan tooas hello **b2c uzantıları uygulaması**, görünür olan *uygulama kayıtlar*. Hello Azure AD B2C hizmet toostore bilgileri kullanıcılar ve özel öznitelikler hakkında tarafından kullanılır. Merhaba uygulama silinirse, Azure AD B2C düzgün çalışmaz ve üretim ortamınıza etkilenecek.

> [!IMPORTANT]
> Kiracı tooimmediately delete planlama sürece hello b2c uzantıları uygulama silmeyin. Merhaba uygulama 30 günden fazla bir süre için silinen kalırsa, kullanıcı bilgilerini kalıcı olarak kaybolur.

## <a name="verifying-that-hello-extensions-app-is-present"></a>Bu hello uzantıları uygulama varsa doğrulanıyor

b2c uzantıları uygulaması hello tooverify bulunmaktadır:

1. Azure AD B2C kiracınızın içinde tıklayın **daha fazla hizmet** hello sol taraftaki gezinti menüsünde.
1. Aramak ve açmak **uygulama kayıtlar**.
1. İle başlayan uygulama Ara **b2c uzantıları uygulaması**

## <a name="recover-hello-extensions-app"></a>Merhaba uzantıları uygulama Kurtar

Merhaba b2c uzantıları uygulama yanlışlıkla sildiyseniz, 30 gün toorecover sahip. Merhaba uygulamasına hello grafik API'sini kullanarak geri yükleyebilirsiniz:

1. Çok Gözat[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).
1. Toohello sitede toorestore silinmiş hello uygulama için istediğiniz hello Azure AD B2C dizini için genel yönetici olarak oturum açın.
1. Bir HTTP GET hello URL karşı sorun `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` api-version ile 1.6 =. Emin tooreplace olun `{tenantName}` Kiracı adınız ile. Bu işlem tüm son 30 gün içinde hello silinmiş hello uygulamaları listeler.
1. 'B2c uzantısı uygulama' ve kopyalama ile Merhaba adı başladığı hello listesinde Hello uygulamayı bulmak, `objectid` özellik değeri.
1. Bir HTTP POST hello URL karşı sorun `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`. Hello yerine `{OBJECTID}` hello URL'sinin hello ile `objectid` hello önceki adımdaki. 

Artık çok gerekir[geri hello uygulama görmek](#verifying-that-the-extensions-app-is-present) hello Azure Portalı'nda.

> [!NOTE]
> Son 30 gün içinde hello silindiyse, uygulamanın yalnızca geri yüklenebilir. 30 günden fazla olması durumunda, verileri kalıcı olarak kaybolur. Daha fazla yardım için destek bileti dosya.
