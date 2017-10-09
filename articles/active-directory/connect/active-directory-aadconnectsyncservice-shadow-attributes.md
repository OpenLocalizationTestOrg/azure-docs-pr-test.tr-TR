---
title: "aaaAzure AD Connect eşitleme hizmeti gölge öznitelikleri | Microsoft Docs"
description: "Gölge öznitelikler Azure AD Connect eşitleme hizmetinin nasıl çalıştığı açıklanmaktadır."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a>Azure AD Connect eşitleme hizmeti gölge öznitelikleri
Çoğu öznitelikleri temsil aynı yolla da hello Azure AD, şirket içi Active Directory'de oldukları gibi. Ancak bazı özel işleme bazı özniteliklere sahip ve Azure AD hello öznitelik değeri Azure AD Connect eşitler daha farklı olabilir.

## <a name="introducing-shadow-attributes"></a>Gölge öznitelikleri Tanıtımı
Bazı öznitelikler Azure AD içinde iki sunumu sahiptir. Merhaba şirket içi değer ve bir hesaplanan değer depolanır. Bu ek öznitelikler gölge öznitelikleri denir. Bu davranış gördüğünüz hello iki en yaygın öznitelikleri **userPrincipalName** ve **proxyAddress**. doğrulanmamış etki alanları temsil eden içinde bu özniteliklerin değerleri olduğunda öznitelik değerleri hello değişiklik olur. Ancak hello eşitleme altyapısı Bağlan hello değerini hello gölge özniteliğinde bunu kendi açısından okur, hello özniteliği Azure AD tarafından onaylanmıştır.

Hello Azure portal veya PowerShell ile kullanarak hello gölge özniteliklerini göremezsiniz. Ancak anlama hello kavram, tootroubleshoot belirli senaryolar farklı değerler şirket içi hello özniteliğine sahip olduğunda ve hello bulutta yardımcı olur.

toobetter hello davranışlarını anlamak, Fabrikam bu örnekten bakın:  
![Etki Alanları](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
Kendi şirket içi Active Directory'de birden çok UPN soneki olabilirler, ancak bunlar yalnızca biri doğruladıktan.

### <a name="userprincipalname"></a>userPrincipalName
Bir kullanıcının öznitelik değerleri doğrulanmamış bir etki alanında aşağıdaki hello sahiptir:

| Öznitelik | Değer |
| --- | --- |
| Şirket içi userPrincipalName | lee.sperry@fabrikam.com |
| Azure AD shadowUserPrincipalName | lee.sperry@fabrikam.com |
| Azure AD userPrincipalName | lee.sperry@fabrikam.onmicrosoft.com |

Merhaba userPrincipalName özniteliği, PowerShell kullanırken gördüğünüz hello değerdir.

Azure AD hello userPrincipalName özniteliği Hello gerçek şirket içi öznitelik değeri zaman hello fabrikam.com etki alanını doğrulayın, Azure AD içinde kaydedildiği hello shadowUserPrincipalName başlangıç değerinden ile güncelleştirir. Güncelleştirilmiş bu değerleri toobe için Azure AD Connect değişiklikleri toosynchronize sahip değil.

### <a name="proxyaddresses"></a>proxyAddresses
Merhaba yalnızca doğrulanmış etki alanlarını dahil etmek için aynı işlemi proxyAddresses, ancak bazı ilave bir mantık daha da oluşur. doğrulanmış etki alanları için Hello onay yalnızca posta kutusu kullanıcılar için gerçekleşir. Bir posta etkin bir kullanıcıya veya kişi temsil eden bir kullanıcı başka bir Exchange kuruluşunda ve proxyAddresses toothese nesnelerindeki değerleri ekleyebilirsiniz.

Her iki şirket içi posta kutusu bir kullanıcı için ya da Exchange Online'da yalnızca değerleri doğrulanmış etki alanları için görünür. Şu şekilde görünebilir:

| Öznitelik | Değer |
| --- | --- |
| Şirket içi proxyAddresses | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| Exchange Online proxyAddresses | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

Bu durumda  **smtp:abbie.spencer@fabrikam.com**  bu etki alanı doğrulanmadı beri kaldırıldı. Ancak aynı zamanda eklenen Exchange  **SIP:abbie.spencer@fabrikamonline.com** . Fabrikam Lync/Skype şirket içi ancak Azure AD kullanmamış ve Exchange Online hazırlamak için.

Başvurulan tooas proxyAddresses için bu mantığı olan **ProxyCalc**. ProxyCalc her değişikliğe bir kullanıcı olarak çağrılan zaman:

- Merhaba kullanıcı hello kullanıcının Exchange için lisanslı değil olsa bile Exchange Online içeren bir hizmet planına atanmıştır. Örneğin, hello kullanıcı atanmışsa Office E3 SKU Merhaba, ancak yalnızca SharePoint Online atanmadı. Posta hala şirket içi olsa bile bu geçerlidir.
- Merhaba özniteliği msExchRecipientTypeDetails bir değer içeriyor.
- Bir değişiklik tooproxyAddresses veya userPrincipalName olun.

ProxyCalc bazı zaman tooprocess bir kullanıcı bir değişiklik alabilir ve hello Azure AD Connect dışarı aktarma işlemine zaman uyumlu değil.

> [!NOTE]
> Bu konudaki belgelenmemiş Gelişmiş senaryolar için bazı ek davranışları Hello ProxyCalc mantığı vardır. Bu konu, toounderstand davranışı hello ve tüm İç mantık belge değil sağlanır.

### <a name="quarantined-attribute-values"></a>Karantinaya alınan öznitelik değerleri
Yinelenen öznitelik değerleri olduğunda gölge öznitelikler de kullanılır. Daha fazla bilgi için bkz: [yinelenen öznitelik dayanıklılık](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="see-also"></a>Ayrıca bkz.
* [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).
