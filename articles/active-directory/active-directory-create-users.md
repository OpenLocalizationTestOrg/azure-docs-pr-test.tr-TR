---
title: "aaaAdd yeni kullanıcılar tooAzure Active Directory | Microsoft Docs"
description: "Açıklar nasıl tooadd yeni kullanıcılar veya Azure Active Directory'de kullanıcı bilgilerini değiştirebilirsiniz."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a>Yeni kullanıcı veya kullanıcıların Microsoft hesaplarını tooAzure Active Directory ile ekleme
Kullanıcıların toopopulate dizininize ekleyin. Bu makalede açıklanır nasıl tooadd yeni kullanıcılar, kuruluşunuzda nasıl ve ne Microsoft hesabına sahip tooadd kullanıcılar. Azure Active Directory'de diğer dizinlerden kullanıcı ekleme veya iş ortağı şirketlerden kullanıcı ekleme hakkında daha fazla bilgi için bkz. [Azure Active Directory'de diğer dizinlerden veya iş ortağı şirketlerden kullanıcılar ekleme](active-directory-create-users-external.md). Eklenen kullanıcılar varsayılan olarak yönetici izinlerine sahip olmayan, ancak herhangi bir zamanda roller toothem atayabilirsiniz.

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. Nasıl tooadd hello Azure AD Yönetim Merkezi'nden bir kullanıcı görmek için [yeni kullanıcılar tooAzure Active Directory eklemek](active-directory-users-create-azure-portal.md).

## <a name="add-a-user"></a>Kullanıcı ekleme
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **Active Directory**ve ardından kuruluş dizininizin hello adını seçin.
3. Select hello **kullanıcılar** sekmesini tıklatın ve ardından hello komut çubuğunda seçin **Kullanıcı Ekle**.
4. Merhaba üzerinde **bu kullanıcı hakkında bize** sayfasında **kullanıcı türünü**, şunlardan birini seçin:

   * **New user in your organization (Kuruluşunuzdaki yeni kullanıcı)** - dizininize yeni bir kullanıcı hesabı ekler.
   * **Var olan bir Microsoft hesabı olan kullanıcı** – mevcut bir Microsoft tüketici hesabını tooyour dizin (örneğin, bir Outlook hesabı) ekler
5. **Type of User (Kullanıcı Türü)** seçeneğine bağlı olarak, bir kullanıcı adı (yeni kullanıcı için) veya bir e-posta adresi (Microsoft hesabı olan bir kullanıcı için) girin.
6. Merhaba kullanıcı **profil** sayfasında, adı ve Soyadı, kullanıcı dostu bir ad ve bir kullanıcı rolüyle hello sağlayın **rolleri** listesi. Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md). Belirtin çok olup olmadığını**çok faktörlü kimlik doğrulamasını etkinleştir** hello kullanıcı için.
7. Merhaba üzerinde **Get geçici parola** sayfasında, **oluşturma**.

> [!IMPORTANT]
> Kuruluşunuz birden fazla etki alanı kullanıyorsa bir kullanıcı hesabı eklediğinizde, sorunları aşağıdaki hello hakkında bilmeniz gerekenler:
>
> * tooadd kullanıcı hesapları ile etki alanları arasında aynı kullanıcı asıl adı (UPN) hello **ilk** ekleme, örneğin, geoffgrisso@contoso.onmicrosoft.com, **arkasından** geoffgrisso@contoso.com.
> * geoffgrisso@contoso.onmicrosoft.com eklemeden önce geoffgrisso@contoso.com **eklemeyin**. Bu sıra önemlidir ve sıkıcı tooundo olabilir.
>
>

## <a name="change-user-information"></a>Kullanıcı bilgilerini değiştirme
Merhaba nesne kimliği dışındaki tüm kullanıcı özniteliklerini değiştirebilirsiniz

1. Dizininizi açın.
2. Select hello **kullanıcılar** sekmesini ve ardından hello görünen adını hello toochange istediğiniz kullanıcı.
3. Değişikliklerinizi tamamlayın ve ardından **Save (Kaydet)** düğmesine tıklayın.

Değiştirdiğiniz hello kullanıcı şirket içi Active Directory hizmetinizle eşitlenmişse bu yordamı kullanarak hello kullanıcı bilgilerini değiştiremezsiniz. toochange hello kullanıcı, şirket içi Active Directory Yönetim araçlarınızı kullanın.

## <a name="guest-user-management-and-limitations"></a>Konuk kullanıcı yönetimi ve sınırlamalar
Konuk, davet edilen tooyour directory tooaccess SharePoint belgeleri, uygulamaları ya da diğer Azure kaynaklarına diğer dizinlerden kullanıcı hesaplarıdır. Bir Konuk hesabı dizininizde çok "konuk." ayarlamak temel alınan UserType özniteliği var Normal kullanıcıların (özellikle de dizininizin üyelerinin) hello UserType özniteliği "Üye" sahip

Konuklar hello dizinde sınırlı bir haklar kümesine sahip. Bu haklar hello özelliği konuklar toodiscover hello dizin diğer kullanıcılar hakkında bilgi edinmek için sınırlar. Ancak, Konuk kullanıcılar hello kullanıcılar ve gruplar üzerinde çalıştığınız hello kaynaklarla ilişkili ile etkileşebilirsiniz. Konuk kullanıcılar şunları yapabilir:

* Diğer kullanıcılar ve gruplar atanmış oldukları bir Azure aboneliği toowhich ile ilişkili bakın
* Ait oldukları gruplar toowhich Hello üyeleri bakın
* Başlangıç dizini, diğer kullanıcıları hello kullanıcı hello tam e-posta adresini biliyorsanız arayın
* Yalnızca sınırlı sayıda sınırlı toodisplay adı, e-posta adresi, kullanıcı asıl adı (UPN) ve küçük resim fotoğrafı yukarı--göründükleri hello kullanıcılar özniteliklerini bakın
* Merhaba dizinde doğrulanan etki alanlarının bir listesini alma
* Dizininizde üyelere sahip aynı erişim izni tooapplications, bunları verme hello

## <a name="set-guest-user-access-policies"></a>Konuk kullanıcı erişim ilkeleri ayarlama
Merhaba **yapılandırma** bir dizinin sekmesi seçenekleri toocontrol konuk kullanıcıların erişimini içerir. Bu seçenekler yalnızca klasik Azure portalında bir dizin genel yöneticisi tarafından değiştirilebilir. Şu anda bir PowerShell veya API yöntemi bulunmamaktadır.

tooopen hello **yapılandırma** hello Azure Klasik portalı, select sekmesinde **Active Directory**ve ardından hello hello dizin adını seçin.

![Azure Active Directory'deki Configure (Yapılandır) sekmesi][1]

Ardından konuk kullanıcıların erişimini hello seçenekleri toocontrol düzenleyebilirsiniz.

![konuk kullanıcılara yönelik erişim denetimi seçenekleri][2]

## <a name="whats-next"></a>Sırada ne var?
* [Azure Active Directory'de diğer dizinlerden veya iş ortağı şirketlerden kullanıcılar ekleme](active-directory-create-users-external.md)
* [Azure AD'yi yönetme](active-directory-administer.md)
* [Azure AD'de parolaları yönetme](active-directory-manage-passwords.md)
* [Azure AD'de grupları yönetme](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
