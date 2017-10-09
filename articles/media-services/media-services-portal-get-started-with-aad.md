---
title: "aaaGet hello Azure portal kullanarak Azure AD kimlik doğrulamasıyla çalışmaya | Microsoft Docs"
description: "Nasıl toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) kimlik doğrulama tooconsume hello Azure Media Services API öğrenin."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak Azure AD kimlik doğrulaması ile çalışmaya başlama

Azure Media Services API toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) kimlik doğrulama tooaccess nasıl hello öğrenin.

## <a name="prerequisites"></a>Ön koşullar

- Bir Azure hesabı. Bir hesabınız yoksa, başlayan bir [Azure ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/). 
- Bir Media Services hesabı. Daha fazla bilgi için bkz: [hello Azure portal kullanarak Azure Media Services hesabı oluşturma](media-services-portal-create-account.md).
- Merhaba gözden emin olun [Azure AD kimlik doğrulamasına genel bakış ile Azure Media Services API erişme](media-services-use-aad-auth-to-access-ams-api.md). 

Azure Media Services ile Azure AD kimlik doğrulaması kullandığınızda, iki kimlik doğrulama seçeneğiniz vardır:

- **Kullanıcı kimlik doğrulaması**. Media Services kaynaklarla hello uygulama toointeract kullanan bir kişi kimlik doğrulaması. Merhaba etkileşimli uygulaması ilk hello kullanıcıdan kimlik bilgilerini ister. Bir örnek yetkili kullanıcıların toomonitor kodlama işlemler tarafından kullanılan bir yönetim konsol uygulaması ya da canlı akış. 
- **Hizmet asıl kimlik doğrulaması**. Bir hizmetin kimliğini. Bu kimlik doğrulama yöntemini yaygın olarak kullanan uygulamaları arka plan programı services, orta katman Hizmetleri veya zamanlanmış işler çalışan uygulamalar şunlardır: web uygulamaları, işlev uygulamalarının, logic apps, API veya bir mikro hizmet.

> [!IMPORTANT]
> Şu anda, Media Services hello Azure erişim denetimi hizmeti kimlik doğrulama modelini destekler. Ancak, erişim denetimi yetkilendirme 1 Haziran 2018 kullanım dışı kalacaktır. Mümkün olan en kısa sürede toohello Azure AD kimlik doğrulama modeli geçirmek öneririz.

## <a name="select-hello-authentication-method"></a>Merhaba kimlik doğrulama yöntemini seçin

1. Merhaba, [Azure portal](https://portal.azure.com/), Media Services hesabınızı seçin.
2. Select nasıl tooconnect toohello Media Services API.

    ![Bağlantı yöntemi sayfası seçin](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a>Kullanıcı kimlik doğrulaması

kullanarak tooconnect toohello Media Services API Merhaba kullanıcı kimlik doğrulaması seçeneği, hello istemci uygulamanın toorequest şu parametreler hello sahip bir Azure AD belirteci gerekir:  

* Azure AD Kiracı uç noktası
* Media Services kaynak URI'si
* Media Services (yerel) uygulama istemci kimliği 
* Media Services (yerel) uygulama yeniden yönlendirme URI'si 
* Kaynak URI'si REST Media Services için

Bu parametrelerin hello üzerinde hello değerleri alabilirsiniz **kullanıcı kimlik doğrulaması ile Media Services API** sayfası. 

![Kullanıcı kimlik doğrulaması sayfası ile bağlanma](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

Hello Media Services Microsoft .NET SDK kullanarak toohello Media Services API bağlanıyorsanız hello değerleri kullanılabilir tooyou hello SDK bir parçası olarak gereklidir. Daha fazla bilgi için bkz: [kullanım Azure AD kimlik doğrulama tooaccess hello .NET ile Azure Media Services API](media-services-dotnet-get-started-with-aad.md).

Merhaba Media Services .NET İstemci SDK kullanmıyorsanız, daha önce bahsedilen hello parametrelerini kullanarak bir Azure AD belirteç isteği el ile oluşturmalısınız. Daha fazla bilgi için bkz: [nasıl toouse hello Azure AD kimlik doğrulama kitaplığı tooget hello Azure AD belirteci](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="service-principal-authentication"></a>Hizmet sorumlusu kimlik doğrulaması

Hizmet asıl seçeneğini kullanarak tooconnect toohello Media Services API Merhaba, orta katman uygulamanızın (web API ya da web uygulaması) toorequest şu parametreler hello sahip bir Azure AD belirteci gerekir:  

* Azure AD Kiracı uç noktası
* Media Services kaynak URI'si 
* Kaynak URI'si REST Media Services için
* Azure AD uygulama değerleri: Merhaba **istemci kimliği** ve **istemci parolası**

Bu parametrelerin hello üzerinde hello değerleri alabilirsiniz **tooMedia Hizmetleri API ile hizmet sorumlusu bağlanmak** sayfası. Bu sayfa toocreate yeni bir Azure kullanın AD uygulaması veya tooselect mevcut bir. Hello Azure AD uygulaması seçtikten sonra hello istemci kimliği (uygulama kimliği) almak ve hello istemci gizli anahtarı (anahtar) değerlerini oluşturmak. 

![Hizmet asıl sayfasıyla Bağlan](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

Ne zaman hello **hizmet sorumlusu** dikey penceresi açıldığında, hello aşağıdaki ölçütleri karşılayan hello ilk Azure AD uygulaması seçili:

- Kayıtlı olan Azure AD uygulaması.
- Katkıda bulunan veya Owner Role-Based erişim denetimi izinleri hello hesabında içeriyor.

Oluşturma veya bir Azure AD uygulaması seçtikten sonra oluşturun ve istemci parolası (anahtar) kopyalayın ve istemci kimliği (uygulama kimliği) hello. Bu senaryoda gerekli tooget hello erişim belirteci Hello istemci gizli anahtarı ve istemci kimliği var.

Etki alanınızda izinleri toocreate Azure AD uygulamalarınız yoksa, hello Azure AD uygulama denetimleri hello dikey gösterilmez ve bir uyarı iletisi görüntülenir.

Media Services API toohello hello Media Services .NET SDK kullanarak bağlanıyorsanız, bkz: [kullanım Azure AD kimlik doğrulama tooaccess hello .NET ile Azure Media Services API](media-services-dotnet-get-started-with-aad.md).

Merhaba Media Services .NET İstemci SDK kullanmıyorsanız, daha önce bahsedilen hello parametrelerini kullanarak bir Azure AD belirteç isteği el ile oluşturmanız gerekir. Daha fazla bilgi için bkz: [nasıl toouse hello Azure AD kimlik doğrulama kitaplığı tooget hello Azure AD belirteci](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="get-hello-client-id-and-client-secret"></a>Merhaba istemci kimliği ve istemci parolası mı almak

Yeni bir tane var olan Azure AD uygulaması veya select hello seçeneği toocreate seçtikten sonra aşağıdaki düğmeler hello görüntülenir:

![İzinler ve Yönet uygulama düğmesi yönetme](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

tooopen hello Azure AD uygulaması dikey penceresinde tıklatın **uygulamasını Yönet**. Merhaba üzerinde **uygulamasını Yönet** dikey penceresinde hello uygulamanın istemci Kimliğini (uygulama kimliği) alabilirsiniz. bir istemci parolası (anahtar), select toogenerate **anahtarları**.

![Uygulama dikey penceresinde anahtarlar seçeneğini yönetme](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a>İzinler ve hello uygulama yönetme

Hello Azure AD uygulaması seçtikten sonra hello uygulama ve izinleri yönetebilirsiniz. tooset diğer uygulamaları, Azure AD uygulama tooaccess tıklatın **izinleri yönetmek**. İçin yönetim görevleri, anahtarları ve yanıt URL'leri ya da tooedit hello uygulamanın bildirim değiştirme gibi tıklatın **uygulamasını Yönet**.

### <a name="edit-hello-apps-settings-or-manifest"></a>Merhaba uygulamanın ayarlarını düzenleyin veya bildirimi

tooedit hello uygulamanın ayarları veya bildirimi tıklatın **uygulamasını Yönet**.

![Uygulamasını Yönet sayfası](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a>Sonraki adımlar

Kullanmaya başlama [tooyour hesabı dosyaları karşıya yükleme](media-services-portal-upload-files.md).
