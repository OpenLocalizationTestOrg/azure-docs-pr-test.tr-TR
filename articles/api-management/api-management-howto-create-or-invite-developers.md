---
title: "aaaHow kullanıcı hesapları Azure API Management'te yönetme | Microsoft Docs"
description: "Bilgi nasıl toocreate veya davet kullanıcılar Azure API Management"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a>Azure API Management'te nasıl toomanage kullanıcı hesapları
API Yönetimi'nde, geliştiricilerin hello API Management kullanarak kullanıma API'leri hello kullanıcılarının önerilir. Bu kılavuzu gösterir toohow toocreate ve davet geliştiriciler toouse hello API'leri ve ürünleri API Management örneğinizle kullanılabilir toothem olun. Merhaba programlı olarak kullanıcı hesaplarını yönetme hakkında daha fazla bilgi için bkz [kullanıcı varlığı](https://msdn.microsoft.com/library/azure/dn776330.aspx) hello belgelerinde [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) başvuru.

## <a name="create-developer"></a>Yeni bir geliştirici oluşturma
toocreate yeni bir geliştirici tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda. Bu toohello API Management yayımcı portalına götürür. Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.

![Yayımcı portalı][api-management-management-console]

Tıklatın **kullanıcılar** hello gelen **API Management** sol hello ve ardından menüsünde **kullanıcı ekleme**.

![Geliştirici oluşturma][api-management-create-developer]

Merhaba girin **e-posta**, **parola**, ve **adı** hello yeni Geliştirici ve tıklatın **kaydetmek**.

![Geliştirici oluşturma][api-management-add-new-user]

Varsayılan olarak, yeni oluşturulan Geliştirici hesaplardır **etkin**ve hello ile ilişkili **geliştiriciler** grubu.

![Yeni Geliştirici][api-management-new-developer]

Geliştirici hesaplarının bir **etkin** durumu kullanılan tooaccess olabilir tüm abonelikleri sahiptirler hello API'leri. Ek gruplarla tooassociate yeni oluşturulan hello Geliştirici bkz [nasıl tooassociate geliştiricilere grupları][How tooassociate groups with developers].

## <a name="invite-developer"></a>Geliştirici davet et
tooinvite bir geliştirici tıklatın **kullanıcılar** hello gelen **API Management** sol hello ve ardından menüsünde **davet kullanıcı**.

![Geliştirici davet et][api-management-invite-developer]

Merhaba Geliştirici Hello adını ve e-posta adresini girin ve tıklayın **davet**.

![Geliştirici davet et][api-management-invite-developer-window]

Bir onay iletisi görüntülenir, ancak bunlar hello daveti kabul ettikten sonra yeni davet hello Geliştirici hello listesi kadar görünmez. 

![Onay davet et][api-management-invite-developer-confirmation]

Bir geliştirici davet e-posta toohello Geliştirici gönderilir. Bu e-posta şablonu kullanılarak oluşturulan ve özelleştirilebilir. Daha fazla bilgi için bkz: [yapılandırma e-posta şablonlarını][Configure email templates].

Merhaba daveti kabul edildikten sonra hello hesabı etkin hale gelir.

## <a name="block-developer"></a> Devre dışı bırakın veya bir geliştirici hesabını yeniden etkinleştirme
Varsayılan olarak, yeni oluşturulan veya davet edilen Geliştirici hesaplardır **etkin**. toodeactivate bir geliştirici hesabını tıklatın **blok**. tooreactivate engellenen Geliştirici hesabını tıklatın **etkinleştirme**. Engellenen Geliştirici hesabını değil hello Geliştirici portalına erişmek veya tüm API'leri çağırın. bir kullanıcı hesabı toodelete tıklatın **silmek**.

![Blok Geliştirici][api-management-new-developer]

## <a name="reset-a-user-password"></a>Kullanıcı parolasını sıfırlama
tooreset hello bir kullanıcı hesabının parolasını hello hello hesabının adını tıklatın.

![Parola sıfırlama][api-management-view-developer]

Tıklatın **parola sıfırlama** toosend bağlantı toohello kullanıcı tooreset parolalarını.

![Parola sıfırlama][api-management-reset-password]

bkz: hello kullanıcı hesapları ile tooprogrammatically çalışma [kullanıcı varlığı](https://msdn.microsoft.com/library/azure/dn776330.aspx) hello belgelerinde [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) başvuru. kullanıcı hesabı parolasını tooa belirli bir değer tooreset, kullanabileceğiniz hello [kullanıcıyı güncelleştirmek](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) işlemi ve hello istenen parolayı belirtin.

## <a name="pending-verification"></a>Bekleyen doğrulama
![Bekleyen doğrulama][api-management-pending-verification]

## <a name="next-steps"> </a>Sonraki adımlar
Bir geliştirici hesabı oluşturulduktan sonra rolleriyle ilişkilendirmek ve tooproducts ve API'leri abone olun. Daha fazla bilgi için bkz: [nasıl toocreate ve kullanım grupları][How toocreate and use groups].

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
