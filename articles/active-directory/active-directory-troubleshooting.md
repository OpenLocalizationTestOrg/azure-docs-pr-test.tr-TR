---
title: "Sorun giderme: 'Active Directory' öğesi eksik veya kullanılabilir değil | Microsoft Docs"
description: "Active Directory menü öğesi hello Azure Yönetim Portalı görünmüyor olduğunda hangi toodo."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a>Sorun giderme: 'Active Directory' öğesi eksik veya kullanılabilir değil
Azure Active Directory özelliklerini ve hizmetlerini kullanma hello yönergeleri çoğunu ile başlayan "toohello Azure yönetim portalına gidin ve tıklayın **Active Directory**." Ancak ne yaparsınız hello Active Directory uzantısına veya menü öğesini görünmüyorsa veya işaretlenmiş olması durumunda **kullanılamaz**? Bu konu tasarlanmış toohelp ilgilidir. Merhaba hangi koşullar altında açıklar **Active Directory** görünmez veya kullanılamaz durumda ve açıklar nasıl tooproceed.

## <a name="active-directory-is-missing"></a>Active Directory eksik
Genellikle, bir **Active Directory** öğesi hello sol gezinti menüsünde görüntülenir. Azure Active Directory yordamları Hello yönergeleri Bu öğe görünümünüzde olduğunu varsayın.

![Ekran görüntüsü: Azure Active Directory'de](./media/active-directory-troubleshooting/typical-view.png)

Aşağıdaki koşullar Merhaba, doğru olduğunda hello Active Directory öğesi hello sol gezinti menüsünde görüntülenir. Aksi takdirde hello öğesi görünmez.

* (önceki adıyla Windows Live ID bilinir) bir Microsoft hesabı ile oturum açmış geçerli kullanıcı hello.
  
    OR
* Hello Azure Kiracı bir dizine sahip ve hello geçerli hesap bir dizin yöneticisidir.
  
    OR
* Hello Azure Kiracı en az bir Azure AD erişim denetimi (ACS) ad alanı vardır. Daha fazla bilgi için bkz: [erişim denetimi Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).
  
    OR
* Hello Azure Kiracı en az bir Azure çok faktörlü kimlik doğrulama sağlayıcısı sahiptir. Daha fazla bilgi için bkz: [yönetme Azure çok faktörlü kimlik doğrulama sağlayıcıları](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

Erişim denetimi ad alanı veya bir çok faktörlü kimlik doğrulama sağlayıcısı toocreate tıklatın **+ yeni** > **uygulama hizmetleri** > **Active Directory**.

tooget yönetici hakları tooa dizin sahip bir yönetici atamak Yönetici rolü tooyour hesabı. Ayrıntılar için bkz [yönetici rolleri atama](active-directory-assign-admin-roles.md).

## <a name="active-directory-is-not-available"></a>Active Directory kullanılabilir değil
Tıkladığınızda **+ yeni** > **uygulama hizmetleri**, bir **Active Directory** öğesi görünür. Özellikle, dizin, erişim denetimi veya çok faktörlü yetki sağlayıcı gibi hello Active Directory özelliklerinden herhangi birini kullanılabilir toohello geçerli kullanıcı olmadığında hello Active Directory öğesi görüntülenir.

Ancak, hello sayfa yüklenirken hello öğesi soluk ve işaretlenmiş **kullanılamaz**. Bu geçici bir durumdur. Birkaç saniye bekleyin, hello öğesi kullanılabilir hale gelir. Merhaba gecikme uzatılırsa yenileme hello web sayfası genellikle hello sorunu giderir.

![Ekran görüntüsü: Active Directory kullanılabilir değil](./media/active-directory-troubleshooting/not-available.png)

