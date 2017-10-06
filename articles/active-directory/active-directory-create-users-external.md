---
title: "diğer dizinlerden veya iş ortağı şirketlerdeki Azure Active Directory'de aaaAdd kullanıcılar | Microsoft Docs"
description: "Açıklar nasıl tooadd kullanıcılar veya Azure Active Directory'de dış ve yeni Konuk kullanıcılar dahil olmak üzere, kullanıcı bilgilerini değiştirebilirsiniz."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 564a04ec-53c1-470b-9ab9-f3db57da0a89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 92099e5792365c307b0f3d4f2dff5dd8424aeab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a>Azure Active Directory'de diğer dizinlerden veya iş ortağı şirketlerden kullanıcılar ekleme

Bu makalede açıklanır nasıl tooadd kullanıcıların Azure Active Directory'de diğer dizinlerden veya iş ortağı şirketlerden kullanıcılar ekleyebilirsiniz. Kuruluşunuzdaki yeni kullanıcı ekleme ve Microsoft hesabına sahip kullanıcıların eklenmesi hakkında daha fazla bilgi için bkz: [yeni kullanıcılar tooAzure Active Directory eklemek](active-directory-create-users.md). 

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. Nasıl tooadd B2B işbirliği Konuk kullanıcılar hello Azure AD Yönetim Merkezi için bkz: [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)

Eklenen kullanıcılar varsayılan olarak yönetici izinlerine sahip olmayan, ancak herhangi bir zamanda roller toothem atayabilirsiniz.

## <a name="add-a-user"></a>Kullanıcı ekleme
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) hello dizin için genel yönetici olan bir hesapla.
2. **Active Directory**'yi seçin ve ardından dizininizi açın.
3. Select hello **kullanıcılar** sekmesini tıklatın ve ardından hello komut çubuğunda seçin **Kullanıcı Ekle**.
4. Merhaba üzerinde **bu kullanıcı hakkında bize** sayfasında **kullanıcı türünü**, şunlardan birini seçin:

   * **Başka bir Azure AD dizinindeki kullanıcı** – başka bir Azure AD dizininden kaynaklanan bir kullanıcı hesabı tooyour dizini ekler. Başka bir dizindeki bir kullanıcıyı yalnızca bu dizinin de bir kullanıcısı olduğunuzda ekleyebilirsiniz.
   * **İş ortağı şirketlerdeki kullanıcılar** -tooinvite ve iş ortağı şirket kullanıcıları tooyour dizin yetkilendirmek (bkz [Azure Active Directory B2B işbirliği](active-directory-b2b-what-is-azure-ad-b2b.md)). Çok gerekir[e-posta adreslerini belirterek bir CSV dosyası yükleme](active-directory-b2b-references-csv-file-format.md).
5. Merhaba kullanıcı **profil** sayfasında, adı ve Soyadı, kullanıcı dostu bir ad ve bir kullanıcı rolüyle hello sağlayın **rolleri** listesi. Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md). Belirtin çok olup olmadığını**çok faktörlü kimlik doğrulamasını etkinleştir** hello kullanıcı için.
6. Merhaba üzerinde **Get geçici parola** sayfasında, **oluşturma**.

> [!IMPORTANT]
> Kuruluşunuz birden fazla etki alanı kullanıyorsa bir kullanıcı hesabı eklediğinizde, sorunları aşağıdaki hello hakkında bilmeniz gerekenler:
>
> * tooadd kullanıcı hesapları ile etki alanları arasında aynı kullanıcı asıl adı (UPN) hello **ilk** ekleme, örneğin, geoffgrisso@contoso.onmicrosoft.com, **arkasından** geoffgrisso@contoso.com.
> * geoffgrisso@contoso.onmicrosoft.com eklemeden önce geoffgrisso@contoso.com **eklemeyin**.
>

Bir kullanıcının kimliği şirket içi Active Directory hizmetinizle eşitlenir bilgilerini değiştirirseniz, hello Klasik Azure portalı hello kullanıcı bilgilerini değiştiremezsiniz. toochange Merhaba kullanıcı bilgileri, şirket içi Active Directory Yönetim araçlarınızı kullanın.

## <a name="add-external-users"></a>Dış kullanıcılar ekleme
Aynı zamanda kullanıcılara ait olduğunuz başka bir Azure AD directory toowhich veya iş ortağı şirketlerden bir CSV dosyasını karşıya yükleyerek ekleyebilirsiniz. tooadd bir dış kullanıcı için **kullanıcı türü**, belirtin **başka bir Microsoft Azure AD dizinindeki kullanıcı** veya **iş ortağı şirketlerdeki kullanıcılar**.

Her iki türdeki kullanıcıların da kaynağı başka bir dizindir ve **dış kullanıcılar** olarak eklenirler. Dış kullanıcılar gereksinim tooadd yeni hesaplar ve kimlik bilgileri olmadan bir dizindeki diğer kullanıcılarla işbirliği yapabilir. Dış kullanıcılar kendi giriş dizininde ile oturum açın ve bu kimlik doğrulaması eklenmiş oldukları diğer tüm dizinleri toowhich için çalışır kimlik doğrulaması.

## <a name="external-user-management-and-limitations"></a>Dış kullanıcı yönetimi ve sınırlamalar
Bir kullanıcı başka bir dizin tooyour dizinden eklediğinizde, bu kullanıcı dizininizde bir dış kullanıcı olur. Merhaba görünen adı ve kullanıcı adı kullanıcının giriş dizininden kopyalanır ve hello dizininizdeki dış kullanıcı için kullanılır. Daha sonra hello dış kullanıcı hesabının özellikleri tamamen bağımsız olur. Özellik değişiklikleri toohello kullanıcı kendi giriş dizininde yapılırsa, bu değişiklikleri yayılmaz toohello dizininizdeki dış kullanıcı hesabı.

Merhaba hello iki hesap arasındaki tek bağlantı, bu hello kullanıcının her zaman zaman kendi giriş dizininde veya Microsoft hesabında kimlik doğrulaması ' dir. İşte bu nedenle bir seçenek tooreset hello parola bakın yok veya bir dış kullanıcı için çok faktörlü kimlik doğrulamasını etkinleştirin. Şu anda hello giriş dizininde veya Microsoft hesabı hello kimlik doğrulama ilkesini hello tek hello kullanıcının oturum açtığı zaman değerlendirilen ' dir.

> [!NOTE]
> Hala erişim tooyour dizin engeller hello dizininde hello dış kullanıcı devre dışı bırakabilirsiniz.
>
>

Bir kullanıcı kendi giriş dizininde silinirse veya Microsoft hesabını iptal ederse, hello dış kullanıcı dizininizde hala vardır. Ancak, bunlar bir giriş dizininde veya Microsoft hesabı ile kimlik doğrulaması yapamadığı için dizininizdeki hello kullanıcı kaynaklarına erişemez.

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a>Şu anda Azure AD dış kullanıcılarının erişimini destekleyen hizmetler
* **Klasik Azure portalı**: birden çok dizin toomanage her bu dizinlerin yöneticisi olan bir dış kullanıcının verir.
* **SharePoint Online**: dış paylaşım etkinleştirilmişse bir dış kullanıcı tooaccess SharePoint Online yetkili kaynaklarına sağlar.
* **Dynamics CRM**: hello kullanıcı PowerShell yoluyla lisanslanmışsa bir dış kullanıcı tooaccess kaynakları Dynamics CRM'deki yetkili sağlar.
* **Dynamics AX**: hello kullanıcı PowerShell yoluyla lisanslanmışsa bir dış kullanıcı tooaccess kaynakları Dynamics AX'teki yetkili sağlar. Merhaba sınırlamalar [Azure AD dış kullanıcılarının](#known-limitations-of-azure-ad-external-users) Dynamics AX tooexternal kullanıcılar da geçerlidir.

## <a name="next-steps"></a>Sonraki adımlar
* [Yeni kullanıcılar tooAzure Active Directory ekleme](active-directory-create-users.md)
* [Azure AD'yi yönetme](active-directory-administer.md)
* [Azure AD'de parolaları yönetme](active-directory-manage-passwords.md)
* [Azure AD'de grupları yönetme](active-directory-manage-groups.md)
