---
title: "Azure Active Directory B2C: Azure Active Directory B2C kiracısı oluşturma | Microsoft Docs"
description: "Nasıl toocreate bir Azure Active Directory B2C Kiracı üzerinde bir konu"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a>Hello Azure portalında bir Azure Active Directory B2C kiracısı oluşturma

Sipi tarafından düzenlenebilir.

Bu Hızlı Başlangıç, yalnızca birkaç dakika içinde bir Microsoft Azure Active Directory (Azure AD) B2C Kiracı oluşturmanıza yardımcı olur. İşlemi tamamladığınızda, B2C uygulamaları kaydettirmek için B2C Kiracı toouse sahip.

## <a name="prerequisites"></a>Ön koşullar

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a>İçinde tooAzure oturum

İçinde toohello oturum [Azure portal](https://portal.azure.com/).

## <a name="create-an-azure-ad-b2c-tenant"></a>Azure AD B2C kiracısı oluşturma

B2C özellikleri, var olan kiracılar etkinleştirilemez. Toocreate Azure AD B2C kiracısı gerekir.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

Tebrikler, Azure Active Directory B2C kiracısı oluşturdunuz. Merhaba Kiracı genel Yöneticisi olduğunuz. Gerektiğinde başka Genel Yöneticiler ekleyebilirsiniz. tooswitch tooyour yeni Kiracı, hello tıklatın *yeni Kiracı bağlantıyı Yönet*.

![Yeni Kiracı bağlantıyı Yönet](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> Toouse bir üretim uygulaması için bir B2C Kiracı planlıyorsanız hello makaleyi okuyun [Önizleme B2C kiracılar ve üretim ölçekli](active-directory-b2c-reference-tenant-type.md). Var. Varolan bir B2C sildiğinizde Kiracı bilinen sorunlar ve hello ile yeniden oluşturmanız aynı etki alanı adı. B2C Kiracı farklı etki alanı adı ile toocreate gerekir.
>
>

## <a name="link-your-tenant-tooyour-subscription"></a>Kiracı tooyour aboneliğinizi Bağla

Toolink gereken Azure AD B2C tooyour Azure aboneliği tooenable tüm B2C işlevselliği Kiracı ve kullanım ücretleri için ödeme yaparsınız. toolearn daha fazlasını okuyun [bu makalede](active-directory-b2c-how-to-enable-billing.md). Azure AD B2C Kiracı tooyour Azure aboneliği bağlarsanız yok, bazı işlevler engellenir ve bir uyarı iletisi ("bağlantılı toothis B2C Kiracı veya abonelik hello abonelik, ilgilenilmesi gerekiyor. hello B2C ayarlarında gerekir") bakın. Üretime uygulamalarınızı sevk önce bu adımı uygulamanız önemlidir.

## <a name="easy-access-toosettings"></a>Kolay erişim toosettings

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

Girerek hello dikey erişebilirsiniz `Azure AD B2C` içinde **arama kaynakları** hello portal hello üstünde. Merhaba sonuçları listesinden seçmek **Azure AD B2C** tooaccess hello B2C ayarlar dikey penceresi.

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [B2C Kiracı B2C uygulamanızı kaydetme](active-directory-b2c-app-registration.md)
