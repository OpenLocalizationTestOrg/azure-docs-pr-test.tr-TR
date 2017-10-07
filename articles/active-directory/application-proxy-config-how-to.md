---
title: Uygulama proxy'si uygulama aaaHow tooconfigure | Microsoft Docs
description: "Bilgi nasıl toocreate bir yapılandırma birkaç basit adımda bir uygulama proxy'si uygulama"
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
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a>Nasıl tooconfigure uygulama proxy'si uygulama

Bu makale toounderstand yardımcı nasıl tooconfigure bir Azure AD tooexpose uygulama proxy'si uygulamadaki şirket içi uygulamalar toohello bulut.

## <a name="recommended-documents"></a>Önerilen belgeler 

Merhaba başlangıç yapılandırmasını ve hello Yönetici portalı üzerinden bir uygulama proxy'si uygulama oluşturma hakkında toolearn izleyin hello [Azure AD uygulama proxy'si ile uygulama yayımlama](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Bağlayıcılar yapılandırma hakkında daha fazla bilgi için bkz [uygulama ara sunucusunu etkinleştirme hello Azure portal](active-directory-application-proxy-enable.md).

Sertifikaları karşıya yükleniyor ve özel etki alanlarını kullanma hakkında daha fazla bilgi için bkz: [Azure AD uygulama proxy'si özel etki alanları ile çalışma](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).

## <a name="create-hello-applicationsetting-hello-urls"></a>Uygulama/ayarı hello URL'leri Hello oluşturma

Merhaba, izliyorsanız hello adımları [Azure AD uygulama proxy'si ile uygulama yayımlama](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) belgelerine ve bu Merhaba uygulaması oluşturulurken bir hata alma hello hata ayrıntıları için bilgi ve ilgili öneriler bakın toofix Merhaba uygulaması. Çoğu hata iletileri önerilen bir düzeltmeyi içerir. tooavoid sık karşılaşılan doğrulayın:

-   Bir yönetici izni toocreate uygulama proxy'si uygulama ile

-   Merhaba İç URL benzersizdir

-   Merhaba dış URL benzersizdir

-   http veya https URL'leri başlangıcı hello ve sonunda bir "/"

-   Merhaba URL bir etki alanı adı, IP adresi olmalıdır

Merhaba uygulaması oluşturduğunuzda hello sağ üst köşedeki hello hata iletisi görüntülenmelidir. Merhaba bildirim simgesine toosee hello hata iletileri de seçebilirsiniz.

   ![Bildirim istemi](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>Bağlayıcılar/bağlayıcı gruplarını yapılandırma

Merhaba bağlayıcılar ve bağlayıcı grupları hakkında uyarı nedeniyle, uygulamanızın yapılandırma zorluk yaşıyorsanız, hakkında ayrıntılar için uygulama proxy'si etkinleştirme hakkında yönergeler Bkz: toodownload bağlayıcılar. Merhaba toolearn bağlayıcılar hakkında daha fazla bilgi istiyorsanız bkz [bağlayıcılar belgelerine](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).

Bağlayıcılar etkin olmayan, bu oluşturulamıyor tooreach hello hizmet oldukları anlamına gelir. Bu, genellikle tüm gereken hello bağlantı noktalarının açık olmadığından olur. toosee gerekli bağlantı noktalarının listesi, uygulama proxy'si belgelerine etkinleştirme hello hello ön koşullar bölümüne bakın.

## <a name="upload-certificates-for-custom-domains"></a>Özel etki alanları için sertifikalarını karşıya yükleme

Özel etki alanları, dış URL'ler toospecify hello etki alanını sağlar. toouse özel etki alanlarını, etki alanında tooupload hello sertifikası gerekir. Özel etki alanları ve sertifikaları kullanma hakkında daha fazla bilgi için bkz: [Azure AD uygulama proxy'si özel etki alanları ile çalışma](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains). 

Sertifikanız karşıya sorunlarla karşılaşıyorsanız hello hata iletileri hello portalında hello sertifikasıyla hello sorun hakkında ek bilgi arayın. Ortak sertifika sorunları şunları içerir:

-   Süresi dolan sertifika

-   Otomatik olarak imzalanan sertifika

-   Sertifika hello özel anahtarı eksik

hello tooupload hello sertifika çalışırken sağ üst köşedeki içinde Hello hata iletisi görüntüler. Merhaba bildirim simgesine toosee hello hata iletileri de seçebilirsiniz.

   ![Bildirim istemi](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>Sonraki adımlar
[Azure AD uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md)
