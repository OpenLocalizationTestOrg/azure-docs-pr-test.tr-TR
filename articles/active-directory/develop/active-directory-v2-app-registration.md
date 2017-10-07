---
title: "aaaRegister hello Azure AD v2.0 uç hello portalı kullanarak bir uygulama | Microsoft Docs"
description: "Nasıl tooregister oturum açma etkinleştirmek ve Microsoft erişmek için Microsoft ile bir uygulama hello v2.0 uç hizmetlerini kullanma"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a>Nasıl tooregister hello v2.0 uç noktası ile uygulama
toobuild MSA & Azure AD kabul eden bir uygulama oturum açma, ilk tooregister Microsoft ile bir uygulama gerekir.  Şu anda olmaz mümkün toouse Azure AD ile olabilecek uygulamalardan mevcut olması veya MSA - toocreate marka yeni bir tane gerekir.

> [!NOTE]
> Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.  Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a>Merhaba Microsoft uygulama kayıt portalı ziyaret edin
İlk şey ilk - gidin çok[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Microsoft uygulamalarınızda yönetebileceği yeni bir uygulama kayıt portalı budur.

Oturum ya da kişisel oturum, iş veya Okul Microsoft hesabı.  Ya da yoksa, yeni bir kişisel hesap için kaydolun. Şimdi, uzun sürmez - biz burada beklemeniz.

Bitti mi? Şimdi Microsoft uygulamaları listesi büyük olasılıkla boş olduğu aramanız.  Değiştirelim.

Tıklatın **bir uygulama ekleyin**ve bir ad verin.  Merhaba portal uygulamanızı daha sonra kodunuzda kullanacağınız genel benzersiz bir uygulama kimliği atar.  Uygulamanızı bir sunucu tarafı bileşeni içeriyorsa, erişim belirteçleri için arama API'leri gerekir (düşünün: Office, Azure veya web API), toocreate isteyeceksiniz bir **uygulama gizli anahtarı** burada da.

Ardından, hello uygulamanızı kullanacağı platformları ekleyin.

* Web tabanlı uygulamalar için bir **yeniden yönlendirme URI'si** burada oturum açma iletiler gönderilemez.
* Mobil uygulamalarda, sizin için otomatik olarak oluşturulan URI hello varsayılan basılı kopya yönlendirin.

İsteğe bağlı olarak, oturum açma sayfanızda hello profil bölümü hello Görünüm ve yapısını özelleştirebilirsiniz.  Emin tooclick olun **kaydetmek** geçmeden önce.

> [!NOTE]
> Kullanarak bir uygulama oluşturduğunuzda [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), Merhaba uygulaması kayıtlı hello ev kiracısında hello hesabının hello Portalı'na toosign kullanın.  Bu, bir uygulamayı kişisel bir Microsoft hesabı kullanarak, Azure AD kiracınızda kaydedebilirsiniz değil, anlamına gelir.  Açıkça tooregister bir uygulama içinde belirli bir kiracı istiyorsanız, ilk Kiracı içinde oluşturulan bir hesapla oturum açın.
> 
> 

## <a name="build-a-quick-start-app"></a>Hızlı Başlangıç uygulaması oluşturma
Bir Microsoft uygulaması sahip olduğunuza göre v2.0 hızlı başlangıç öğreticilerimizden birini tamamlayabilirsiniz.  İşte birkaç öneri:

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

