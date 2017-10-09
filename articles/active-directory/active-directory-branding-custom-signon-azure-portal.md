---
title: "oturum açma işleminiz sayfa hello Azure Active Directory aaaCustomize | Microsoft Docs"
description: "Bilgi nasıl tooadd şirket markasıyla toohello Azure oturum açma sayfası"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a>Şirket tooyour oturum açma sayfasında hello Azure Active Directory markası ekleme
tooavoid Karışıklığı önlemek için birçok şirket tüm hello Web siteleri ve yönettikleri hizmetlerde tooapply tutarlı bir görünüm istiyor. Azure Active Directory toocustomize hello hello oturum açma sayfası şirket Logonuzla ve özel renk düzenleri görünümünü sağlayarak bu yeteneği sağlar. Merhaba oturum açma sayfası 365 veya Azure AD kimlik sağlayıcınız olarak kullanan diğer web tabanlı uygulamalar tooOffice içinde oturum açtığınızda görüntülenen hello sayfasıdır. Kimlik bilgilerinizi bu sayfayı tooenter ile etkileşim.

Şirketinizin markasını, renklerini ve diğer özelleştirilebilir öğelerini bu sayfadaki tooshow istiyorsanız, hello iki deneyim arasındaki görüntüleri toounderstand hello fark aşağıdaki hello bakın.

Merhaba ekran gösterir ve örnek hello Office 365 oturum açma sayfasında bir masaüstü bilgisayar için aşağıdaki **önce** bir özelleştirme:

![Özelleştirmeden önce Office 365 oturum açma sayfası](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

Merhaba ekran gösterir ve örnek hello Office 365 oturum açma sayfasında bir masaüstü bilgisayar için aşağıdaki **sonra** bir özelleştirme:

![Özelleştirmeden sonra Office 365 oturum açma sayfası](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a>Merhaba oturum açma sayfasını özelleştirme
Genellikle, tarayıcı tabanlı erişim tooyour bulut uygulamalarınıza ve kuruluşunuzun abonesi olduğu hizmetlere gerekiyorsa, hello oturum açma sayfasını kullanın.

Değişiklikleri tooyour oturum açma sayfası uyguladıysanız, tooan saat hello değişiklikleri tooappear için yukarı alabilir.

Bir hizmeti, https://outlook.com/**contoso**.com veya https://mail.**contoso**.com gibi yalnızca kiracıya özgü bir URL ile ziyaret ettiğinizde markalı oturum açma sayfası görüntülenir.

Hizmeti https://mail.office365.com gibi kiracıya özgü olmayan bir URL ile ziyaret ederseniz markasız oturum açma sayfası görüntülenir. Bu durumda markanız, kullanıcı kimliğinizi girdiğinizde veya kullanıcı kutucuğunu seçtiğinizde görüntülenir.

> [!NOTE]
> * Etki alanı adınızı hello "Etkin" olarak görünmesi gereken **etki alanları** kısmı hello yapılandırılmış markalama Azure portalı. Daha fazla bilgi için bkz: [özel etki alanı adlarını Ekle](active-directory-domains-add-azure-portal.md).
> * Oturum açma sayfası markalama toohello tüketici oturum açma sayfasına Microsoft üzerinden taşımak değil. Bir Microsoft hesabıyla oturum açarsanız Azure AD tarafından işlenen kullanıcı kutucuklarının markalı bir listesini görebilirsiniz ancak kuruluşunuzun hello markası toohello Microsoft hesabı oturum açma sayfasına uygulanmaz.
>
>

Oturum açma sayfanızda hello **Oturumumu açık bırak** onay kutusunu kapatın ve yeniden tarayıcısında açın açtığınız kullanıcı tooremain sağlar.

   ![Oturumum açık kalsın](./media/active-directory-branding-custom-signon-azure-portal/01.png)

Bu durum oturum ömrünü etkilemez. Oturum açma hello Azure Active Directory sayfasında hello onay kutusunu gizleyebilirsiniz.
Merhaba onay kutusu görüntülenip görüntülenmeyeceğini, hello ayarına bağlıdır **Oturumumu devre dışı açık tutmak**.

   ![Oturumum açık kalsın](./media/active-directory-branding-custom-signon-azure-portal/02.png)

toohide onay kutusunu Merhaba, bu çok ayarını yapılandırmak**Evet**.

> [!NOTE]
> Bu kutu mümkün toocheck olan kullanıcılar SharePoint Online ve Office 2010 bazı özelliklerine bağlıdır. Bu ayar toohidden yapılandırırsanız, kullanıcılarınızın ek ve beklenmeyen komut istemlerini toosign de görebilirsiniz.
>
>

**tooadd şirket markasıyla tooyour dizini:**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.

   ![Açılış kullanıcı yönetimi](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **şirket markası**.
4. Merhaba üzerinde **kullanıcılar ve gruplar - şirket markası** dikey penceresinde, select hello **Düzenle** komutu.

    ![Özel marka Düzenle](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. Toocustomize istediğiniz hello öğeleri değiştirin. Tüm öğeler isteğe bağlıdır.
6. **Kaydet** düğmesine tıklayın.

Oturum açma toohello yapılan değişiklikler marka tooappear sayfa için tooan saat sürebilir.

## <a name="next-steps"></a>Sonraki adımlar
[Dile özgü şirket markası ekleme](active-directory-branding-localize-azure-portal.md)
