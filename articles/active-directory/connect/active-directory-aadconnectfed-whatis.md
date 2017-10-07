---
title: aaaAzure AD Connect ve Federasyon | Microsoft Docs
description: "Azure AD Connect kullanan AD FS işlemleri ile ilgili tüm belgeleri için merkezi konumda hello sayfasıdır."
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a>Azure AD Connect ve federasyon
Federasyon ile yapılandırmanıza azure Active Directory (Azure AD) Bağlan olanak şirket içi Active Directory Federasyon Hizmetleri (AD FS) ve Azure AD. Federasyon ile oturum açma, kullanıcıların toosign tooAzure AD tabanlı Services ile şirket içi parolalarını--ve hello kurumsal ağ içindeyken üzerinde tooenter parolalarını yeniden gerek kalmadan etkinleştirebilirsiniz. AD FS ile Merhaba Federasyon seçeneğini kullanarak, yeni bir AD FS yüklemesini dağıtabilir veya bir Windows Server 2012 R2 grubunda varolan bir yüklemesini belirtebilirsiniz.

Bu konuda hello olan Azure AD Connect Federasyon ile ilgili işlevler hakkında bilgi için giriş. Bağlantıları listeler tooall ilgili konular. Bağlantılar tooAzure AD Connect, bkz: [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).

## <a name="azure-ad-connect-federation-topics"></a>Azure AD Connect: Federasyon konuları
| Konu | Ne kapsar ve ne zaman tooread, |
|:--- |:--- |
| **Azure AD Connect kullanıcı oturum açma seçenekleri** | |
| [Kullanıcı oturum açma seçeneklerini anlama](active-directory-aadconnect-user-signin.md) |Çeşitli kullanıcı oturum açma seçenekleri ve hello Azure oturum açma kullanıcı deneyimini nasıl etkilediklerini hakkında bilgi edinin. |
| **Azure AD Connect kullanarak AD FS yükleme** | |
| [Önkoşullar](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |Azure AD Connect yoluyla başarılı bir AD FS yüklemesi Hello önkoşullara bakın. |
| [Bir AD FS grubunu yapılandırma](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |Yeni bir AD FS grubunu, Azure AD Connect kullanarak yükleyin. |
| [Alternatif oturum açma Kimliğini kullanarak Azure AD ile birleştirmek](active-directory-aadconnect-federation-management.md#alternateid) | Alternatif oturum açma Kimliğini kullanarak Federasyon yapılandırma  |
| **Merhaba AD FS yapılandırmasını Değiştir** | |
| [Onarım hello güven](active-directory-aadconnect-federation-management.md#repairthetrust) |Onarım hello geçerli güven arasında AD FS ve Office 365/Azure şirket içi. |
| [Yeni bir AD FS Sunucusu Ekle](active-directory-aadconnect-federation-management.md#addadfsserver) |İlk yüklemeden sonra ek bir AD FS sunucu içeren bir AD FS grubunu genişletin. |
| [Yeni bir AD FS WAP Sunucusu Ekle](active-directory-aadconnect-federation-management.md#addwapserver) |İlk yüklemeden sonra ek bir Web uygulaması Ara sunucusu (WAP) sunucu içeren bir AD FS grubunu genişletin. |
| [Yeni bir Federasyon etki alanına ekleme](active-directory-aadconnect-federation-management.md#addfeddomain) |Azure AD ile birleştirildiyse başka bir etki alanı toobe ekleyin. |
| [Merhaba SSL sertifikasını güncelleştir](active-directory-aadconnectfed-ssl-update.md)| Merhaba SSL sertifikası için bir AD FS grubunu güncelleştirin. |
| **Başka bir Federasyon yapılandırma** | |
| [Azure AD’nin birden çok örneğini tek bir AD FS örneği ile birleştirme](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | Birden çok Azure AD ile tek bir AD FS grubunu birleştirmek| 
| [Bir özel şirket logosu/çizim Ekle](active-directory-aadconnect-federation-management.md#customlogo) |Merhaba oturum açma deneyimini hello AD FS oturum açma sayfasında gösterilen hello özel logo belirterek değiştirin. |
| [Bir oturum açma açıklama ekleme](active-directory-aadconnect-federation-management.md#addsignindescription) |Oturum açma Hello açıklama hello AD FS oturum açma sayfasında değiştirin. |
| [AD FS talep kuralları değiştirme](active-directory-aadconnect-federation-management.md#modclaims) |Değiştirme veya tooAzure AD Connect eşitleme yapılandırması karşılık gelen AD FS'de talep kuralları ekleme. |


## <a name="additional-resources"></a>Ek kaynaklar
* [Federasyonunu iki Azure AD tek AD FS ile](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [Azure AD FS dağıtımı](active-directory-aadconnect-azure-adfs.md)
* [Azure Traffic Manager ile azure'da yüksek kullanılabilirlik çapraz coğrafi AD FS dağıtımı](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
