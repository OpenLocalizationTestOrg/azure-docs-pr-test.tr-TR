---
title: "Azure RemoteApp ile Office 365 kullanıcı hesaplarını kullanma | Microsoft Docs"
description: "Azure RemoteApp ile my Office 365 kullanıcı hesaplarını kullanmayı öğrenin"
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
ms.openlocfilehash: 1bc8949c236afd03415f961cf7a657d4d3926b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-remoteapp-with-office-365-user-accounts"></a>Azure RemoteApp ile Office 365 kullanıcı hesaplarını kullanma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Bir Office 365 aboneliğiniz varsa Azure Active kullanıcı adları ve Office 365 hizmetlerine erişmek için kullanılan parolalar depolayan Directory gerekir. Kullanıcılarınız Office 365 ProPlus etkinleştirdiğinizde Örneğin, bunlar için lisans denetlemek için Azure ad kimlik doğrulaması. Müşterilerin çoğu, Azure RemoteApp ile aynı dizinde kullanmak istersiniz.

Azure RemoteApp dağıtıyorsanız farklı bir Azure AD ile ilişkili bir Azure aboneliği büyük olasılıkla kullanıyor. Office 365 dizininize kullanabilmeniz için bu dizine Azure aboneliği taşımanız gerekir.

Office 365 istemci uygulamaları dağıtma hakkında daha fazla bilgi için bkz: [Azure RemoteApp ile Office 365 aboneliğinizi kullanma](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>1. Aşama: ücretsiz, Office 365 Azure Active Directory abonelik kaydı
Klasik Azure portalını kullanıyorsanız, içindeki adımları kullanın [ücretsiz Azure Active Directory aboneliğinizi kaydetmek](https://technet.microsoft.com/library/dn832618.aspx) Azure Yönetim Portalı aracılığıyla Azure AD yönetim erişmek için. Bu işlem sonucu olarak Azure portalında oturum açın ve Azure RemoteApp ile kullandığınız tam Azure aboneliği farklı bir dizinde olduğundan, çok daha bu noktada görmezsiniz dizininiz var. – bkz yapabiliyor olmanız gerekir.

Bu adımda oluşturduğunuz yönetici hesabının parolasını ve adını anımsamak – Aşama 2'de gerekecektir.

Azure portalını kullanıyorsanız, kullanıma [kaydetmek ve bir ücretsiz Azure Office 365 portalı kullanarak Active Directory etkinleştirmek nasıl](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-the-azure-ad-associated-with-your-azure-subscription"></a>2. Aşama: Azure aboneliğinizle ilişkili Azure AD değiştirin.
1. aşaması biz çalışılan ile Office 365 dizine geçerli dizinden Azure aboneliğinizi değiştirme olacak.

Bölümünde açıklanan yönergeleri izleyin [Azure remoteapp'te Azure Active Directory kiracısını değiştirme](remoteapp-changetenant.md). Belirli aşağıdaki adımları dikkat edin:

* #1. adım: Bu abonelikte Azure RemoteApp (ARA) dağıttıysanız, Azure AD kullanıcı hesaplarının tümünü tüm ARA koleksiyonlarından ilk olarak, başka bir şey denemeden önce kaldırdığınız emin olun. Alternatif olarak, var olan tüm koleksiyonlar silme düşünebilirsiniz.
* #2. adım: Bu önemli bir adımdır. Bir Microsoft hesabı kullanmanız gerekir (örneğin @outlook.com) herhangi bir kullanıcı hesabı için abonelik – bağlı mevcut Azure AD'den sahip olamaz; abonelikte Hizmet Yöneticisi olarak bu çünkü bunu biz farklı bir Azure AD ile taşımak mümkün olmayacaktır.
* #4. adım: varolan bir dizin eklerken, sistem dizin için Yönetici hesabınızla oturum açmak için istenir. 1. aşaması yönetici hesabından kullandığınızdan emin olun.
* #5. adım: Office 365 dizininize aboneliğin üst dizini değiştirin. Sonuç olmalıdır ayarları altında Office 365 dizini aboneliğinizi listeler abonelikleri ->. 
  ![Aboneliğin üst dizini değiştirin](./media/remoteapp-o365user/settings.png)

Bu noktada Azure RemoteApp aboneliğiniz, Office 365 Azure AD ile ilişkili değil; Azure RemoteApp ile mevcut Office 365 kullanıcı hesaplarını kullanabilirsiniz!

