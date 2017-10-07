---
title: "aaaAzure AD + Azure RemoteApp için Active Directory gereksinimleri | Microsoft Docs"
description: "Bilgi nasıl tooset Azure RemoteApp ile Active Directory toowork ayarlama."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Azure AD + Azure RemoteApp için Active Directory gereksinimleri
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp karma koleksiyonu veya toofederate AD Connect kullanarak istediğiniz bulut koleksiyonu toodo hello aşağıdaki gerekir.

### <a name="connect-azure-ad-and-active-directory"></a>Azure AD connect ve Active Directory
Azure AD kiracınıza ve şirket içi Active Directory ortamınızı tooconnect istiyorsanız, AD Connect kullanın. Bu, yalnızca sürer [4 tıklama](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello iki dizini.

Not - dizin eşitleme karma koleksiyonlar için gereklidir.

### <a name="make-sure-your-domaincom-match"></a>Emin olun, "@domain.com" eşleşmesi
Başlamadan önce şirket içi orman eşleşmeleri hello soneki Azure AD etki alanınızın bu Merhaba UPN emin olun. 

Azure AD'de hello UPN etki alanı soneki ayarladıktan sonra Azure Remoteapp'te oturum açan tüm kullanıcılar olarak oturum açacak "kullanıcı @<hello suffix you set up>." Kullanıcılar ayrıca oturum hello aynı oturum emin emin olun user@suffix hello şirket içi etki alanına. Belirli durumlarda bir etki alanı adı hello kullanıcı-tesis içi için farklı bir etki alanı sonekini belirten sırasında Azure AD'de ayarlayabilirsiniz Bu durumda, kullanıcılarınızın mümkün tooconnect tooany etki alanına katılmış bilgisayarlara veya Azure RemoteApp aracılığıyla kaynaklara olmayacaktır.

Örneğin, UPN etki alanı soneki AAD contoso.com olarak ayarlamak, ancak şirket içi/AD üzerinde bazı kullanıcılar ile yapılandırılmış toolog @contoso.uk, bu kullanıcıların hello ARA koleksiyonu mümkün toocorrectly günlüğüne olmaz. Kullanıcıların UPN AAD ve AD olmalıdır aynı hello oturum açma toobe olası hello"

### <a name="create-objects-for-azure-remoteapp"></a>Azure RemoteApp için nesneleri oluşturma
Ayrıca şirket içi Active Directory nesnelerini aşağıdaki toocreate hello gerekir:

* Bir hizmet hesabı tooprovide toodomain erişimine RDSH bitiş noktalarını toohello şirket içi etki alanına katılarak RemoteApp programları.
* Bir kuruluş birimi (OU) toocontain RemoteApp makine nesnesi. Önerilen (ancak gerekli değildir) tooisolate hello hesaplar ve ilkeler, RemoteApp ile kullanacağınız hello OU kullanımıdır.

RemoteApp koleksiyonunuzun oluşturduğunuzda, bu nesnelerin her ikisi gerekir böylece emin toodo adımları ilk olabilir.

