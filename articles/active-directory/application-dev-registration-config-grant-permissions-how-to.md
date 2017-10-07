---
title: "aaaHow toogrant izinleri tooa özel geliştirilmiş uygulama | Microsoft Docs"
description: "Nasıl toogrant izinleri tooyour özel geliştirilmiş uygulama kullanarak hello Azure AD portalı veya bir URL parametresi"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a>Nasıl toogrant izinleri tooa özel geliştirilmiş uygulama

Toogrant izin erken önlem uygulamanıza istediğiniz veya bir hata, tooan uygulama rıza değil, çalışan, aşağıdaki adımları deneyin.

## <a name="how-tooperform-admin-consent-for-your-application"></a>Nasıl uygulamanız için yönetici onayı tooperform

Bu, kuruluşunuzdaki tüm kullanıcılar için onay toohello uygulama verme hello etkisi yoktur.

1. Toohello gidin **uygulama kayıtlar** dikey olarak bir **genel yönetici**seçeneğini belirleyip hello uygulama.

2. Seçin **gerekli izinler**ve son olarak, hello isabet **izinler** hello dikey penceresinde hello üstündeki düğmesi.

Alternatif olarak, bir istek çok oluşturabileceğiniz*login.microsoftonline.com* uygulama yapılandırmaları ile ve üzerinde ilave *& komut istemi Yönetim =\_onayı*. Yönetici kimlik bilgileriyle oturum sonra hello uygulama tüm kullanıcılar için izin verildi.

## <a name="how-tooforce-user-consent-for-your-application"></a>Nasıl tooforce kullanıcı onayı uygulamanız için

* Kimlik doğrulama istekleri ekleme *& sor onay =* kimlik doğrulaması her zaman son kullanıcıların tooconsent gerektirir.

## <a name="next-steps"></a>Sonraki adımlar

[İzin ve tümleştirme uygulamalarını tooAzureAD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[İzin ve adının Azuread'i v2.0 için uygulamalar Yakınsanan](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[Azuread'i StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
