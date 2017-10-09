---
title: "Office 365 kullanıcı hesapları olan aaaHow toouse Azure RemoteApp | Microsoft Docs"
description: "Bilgi nasıl toouse Azure RemoteApp my Office 365 kullanıcı hesapları"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a>Nasıl toouse Azure RemoteApp ile Office 365 kullanıcı hesapları
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Bir Azure Active kullanıcı adlarınız depolayan Directory sahip bir Office 365 aboneliğiniz varsa ve parolaları tooaccess Office 365 hizmetleri kullanılan istiyorsanız. Kullanıcılarınız Office 365 ProPlus etkinleştirdiğinizde Örneğin, Azure AD toocheck lisansları karşı doğrularlar. Müşterilerin çoğu toouse gibi aynı hello Azure RemoteApp ile dizin.

Azure RemoteApp dağıtıyorsanız farklı bir Azure AD ile ilişkili bir Azure aboneliği büyük olasılıkla kullanıyor. Office 365 dizininize toouse sipariş, toomove hello bu dizine Azure aboneliği gerekir.

Konusunda bilgi için bkz: toodeploy Office 365 istemci uygulamaları, [nasıl toouse Azure RemoteApp ile Office 365 aboneliğinize](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>1. Aşama: ücretsiz, Office 365 Azure Active Directory abonelik kaydı
Hello Azure Klasik portalı kullanıyorsanız, hello adımlarda kullanın [ücretsiz Azure Active Directory aboneliğinizi kaydetmek](https://technet.microsoft.com/library/dn832618.aspx) hello Azure Yönetim Portalı aracılığıyla tooget yönetimsel erişim tooyour Azure AD. Merhaba bu işlem sonucunda hello Azure portal içine mümkün toolog olması ve hello Azure RemoteApp ile kullandığınız tam Azure aboneliği farklı bir dizinde olduğundan, çok daha bu noktada görmezsiniz dizininiz var. – konusuna bakın.

Merhaba adını ve bu adımda oluşturduğunuz hello yönetici hesabının parolasını anımsamasını – Aşama 2'de gerekecektir.

Hello Azure portalını kullanıyorsanız, kullanıma [nasıl tooregister ve bir ücretsiz Azure Office 365 portalı kullanarak Active Directory etkinleştirme](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a>2. Aşama: Değişiklik hello Azure AD, Azure aboneliğinizle ilişkilendirilmiş.
Biz toochange, Azure aboneliğinizin geçerli dizinden biz Aşama 1'de çalıştığınız hello Office 365 dizine adımıdır.

Açıklanan hello yönergeleri [değişiklik hello Azure Active Directory kiracısı Azure remoteapp'te](remoteapp-changetenant.md). Aşağıdaki adımları özellikle dikkat toohello ödeme:

* #1. adım: Bu abonelikte Azure RemoteApp (ARA) dağıttıysanız, Azure AD kullanıcı hesaplarının tümünü tüm ARA koleksiyonlarından ilk olarak, başka bir şey denemeden önce kaldırdığınız emin olun. Alternatif olarak, var olan tüm koleksiyonlar silme düşünebilirsiniz.
* #2. adım: Bu önemli bir adımdır. Toouse bir Microsoft hesabı gerekir (örneğin @outlook.com) hello bunu Azure AD bağlı toohello abonelik – var olan tüm kullanıcı hesaplarının sahip olamaz olarak bir Hizmet Yöneticisi hello abonelikte; Bunun nedeni biz mümkün toomove olmayacaktır, tooa farklı Azure AD.
* #4. adım: varolan bir dizin eklerken hello sistem toosign hello yönetici hesabıyla oturum dizin için istenir. Aşama 1'den emin toouse hello yönetici hesabı olun.
* #5. adım: hello abonelik tooyour Office 365 dizininin hello üst dizini değiştirin. Merhaba sonuç olmalıdır ayarları altında aboneliğinizi hello Office 365 dizini listeler abonelikleri ->. 
  ![Merhaba aboneliğin Hello üst dizini değiştirin](./media/remoteapp-o365user/settings.png)

Bu noktada Azure RemoteApp aboneliğiniz, Office 365 Azure AD ile ilişkili değil; Azure RemoteApp ile Merhaba mevcut Office 365 kullanıcı hesaplarını kullanabilirsiniz!

