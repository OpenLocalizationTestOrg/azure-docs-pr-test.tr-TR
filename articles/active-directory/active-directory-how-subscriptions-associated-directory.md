---
title: "aaaHow Azure abonelikleri Azure Active Directory ile ilişkisi | Microsoft Docs"
description: "TooMicrosoft Azure imzalama ve ilgili sorunlar gibi bir Azure aboneliği ve Azure Active Directory arasında hello ilişki."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a>Azure aboneliklerinin Azure Active Directory ile ilişkisi
Bu makalede, bir Azure aboneliği ve Azure Active Directory (Azure AD) arasındaki hello ilişki hakkında bilgi yer almaktadır ve nasıl tooadd var olan bir abonelik tooyour Azure AD dizini.

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a>Azure aboneliğinizin ilişki tooAzure AD
Azure aboneliğiniz hello dizin tooauthenticate kullanıcılar, hizmetler ve cihazlar güvenleri, bunun anlamı Azure AD ile bir güven ilişkisi vardır. Birden çok abonelik hello güvenebileceği aynı dizinde, ancak her abonelik yalnızca bir dizine güvenir. 

Bir aboneliğin bir dizinle arasındaki hello güven ilişkisi diğer kaynaklarla (Web siteleri, veritabanları ve benzeri) Azure sahip hello ilişki benzemez. Bir aboneliğin süresi dolarsa toohello erişim hello aboneliği ile ilişkili diğer kaynaklar da durdurur. Ancak bir Azure AD dizin Azure içinde kalır ve farklı bir aboneliği bu dizinle ilişkilendirebilir ve hello yeni abonelik kullanarak hello dizini yönetme.

![abonelik ilişkileri diyagramı](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

Tüm kullanıcılar kimliklerini doğrulayan tek giriş dizinine sahiptir ancak diğer dizinlerde konuk da olabilmektedir. Azure AD'de kullanıcı hesabınızın üye veya konuk olduğu hello dizinleri görebilirsiniz.

## <a name="azure-ad-and-cloud-service-subscriptions"></a>Azure AD ve bulut hizmeti abonelikleri
Azure AD hello çekirdek dizin ve kimlik yönetimi özellikleri dahil olmak üzere Microsoft bulut hizmetlerinin çoğu arkasında sağlar:

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

Bu Microsoft bulut hizmetlerinden herhangi biri için kaydolurken hello ücretsiz Azure AD hizmeti alın. Bir ek Azure aboneliği tooan Azure AD dizini tooadd istiyorsanız, bir Microsoft hesabıyla oturum imzalanması gerekir. Oturum açma tooAzure bir iş veya Okul hesabı varsa, iş veya Okul hesabınızı doğrudan Azure tarafından doğrulayamadığından Azure aboneliği tooan varolan bir dizin eklenemiyor. 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a>tooadd var olan bir abonelik tooyour Azure AD dizini
Hangi hello ile aboneliğinin ilişkili olduğu her iki hello geçerli dizinde var. bir hesapla oturum açmanız gerekir ve hello dizininde tooadd istediğiniz şekilde. 

1. İçinde toohello oturum [Azure hesap Merkezi](https://account.windowsazure.com/Home/Index) hello aboneliğin Hesap Yöneticisi sahipliği hello bir hesap ile tootransfer istiyor.
2. Hedeflenen hello dizinde toobe hello abonelik sahibi olan isteyen bu hello kullanıcı emin olun.
3. **Aboneliği devret**'e tıklayın.
4. Merhaba alıcı belirtin. Merhaba alıcı otomatik olarak kabul bağlantı içeren bir e-posta alır.
5. Merhaba alıcı hello bağlantıya tıklar ve ödeme bilgilerini girme dahil hello yönergeleri izler. Merhaba alıcı başarılı olduğunda hello abonelik aktarılır. 
6. Merhaba varsayılan dizin hello aboneliğin değiştirildiğinde hello kullanıcı toohello dizindir içinde.


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a>Bir abonelik hem bir dizin önerileri toomanage
bir Azure aboneliğine yönelik yönetim rolleri Hello bağlantılı kaynakları toohello Azure aboneliği yönetin. Bu bölümde Azure aboneliği yöneticilerinin ve Azure AD dizini yöneticilerinin arasındaki hello farklar açıklanmaktadır. Yönetici rolleri ve aboneliğinizi adresindeki ele alınmıştır toomanage kullanmak için diğer öneriler [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles.md).

Varsayılan olarak, kaydolduğunuzda hello Hizmet Yöneticisi rolü atanır. Diğerleri de toosign gerekir ve hello kullanarak hizmetlere erişim aynı abonelik bunları ekleyebileceğiniz ortak yönetici olarak. 

Azure AD yönetim rolleri toomanage hello dizin ve kimlik güvenlikle ilgili özellikler farklı bir dizi vardır. Örneğin, bir dizinin genel Yöneticisi hello kullanıcıları ve grupları toohello dizin ekleyebilir veya kullanıcılar için çok faktörlü kimlik doğrulaması gerektirir. Bir dizin oluşturan bir kullanıcı toohello genel Yönetici rolüne atanır ve tooother kullanıcılara yönetici rolleri atayabilir. Azure AD yönetim rolleri aynı zamanda Office 365 ve Microsoft Intune gibi diğer hizmetler tarafından da kullanılır. 

Azure aboneliği yöneticilerinin ve Azure AD dizini yöneticilerinin iki farklı rol olmasıdır. 
* Azure aboneliği yöneticileri, azure'daki kaynakları yönetebilir ve (hello Azure portal kendisini bir Azure kaynağı olduğundan) Azure AD hello Azure portalını kullanabilirsiniz. 
* Dizin yöneticileri hello Azure AD dizini yalnızca özelliklerinde yönetebilirsiniz.

Bir kişi her iki rolde de olabilir ancak bu gerekli değildir. Dizin genel yöneticisi, hizmet yöneticisi veya bir Azure aboneliğinin ortak yöneticisi olarak atanamaz. Bu durumun tersi de geçerlidir. Yönetici hello aboneliğin olmaksızın hello kullanıcı toohello Azure portalında oturum açabilir, ancak hello Portalı'nda bu abonelik için hello dizinleri yönetemezler. Ancak, bu kullanıcı dizinleri Azure AD PowerShell veya hello Office 365 Yönetici merkezi gibi diğer araçları kullanarak yönetebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* toolearn nasıl toochange Yöneticiler bir Azure aboneliğine yönelik bakın hakkında daha fazla bilgi [bir Azure aboneliği tooanother hesap sahipliğini aktarma](../billing/billing-subscription-transfer.md)
* Microsoft Azure'da kaynak erişiminin nasıl denetlendiğini hakkında daha fazla toolearn bkz [azure'da kaynak erişimini anlama](active-directory-understanding-resource-access.md)
* Hakkında daha fazla bilgi için bkz: tooassign rolleri Azure AD'de [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
