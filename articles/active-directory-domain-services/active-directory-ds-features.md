---
title: "Azure Active Directory etki alanı Hizmetleri: Özellikleri | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri özellikleri"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8d1c3eb3-1022-4add-a919-c98cc6584af1
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1a9417bafa35959d280eabf3db6ad8530db4ea45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD Domain Services
## <a name="features"></a>Özellikler
özellikler aşağıdaki hello Azure AD etki alanı Hizmetleri yönetilen etki alanlarında kullanılabilir.

* **Basit Dağıtım deneyimi:** yalnızca birkaç tıklama kullanarak Azure AD kiracınız için Azure AD Etki Alanı Hizmetleri'ni etkinleştirebilirsiniz. Azure AD kiracınıza bulut Kiracı olup şirket içi dizininize ile eşitlenen bağımsız olarak, yönetilen etki alanınızı hızlı bir şekilde sağlanabilir.
* **Etki alanına katılma için destek:** hello yönetilen etki alanınızı bulunan Azure sanal ağı etki alanına katılma bilgisayarları kolayca. Windows istemci ve sunucu işletim sistemleri works sorunsuz bir şekilde Azure AD etki alanı Hizmetleri tarafından hizmet verilen etki alanları karşı Hello etki alanına katılım deneyimi. Bu tür etki alanlarına yönelik tooling otomatik etki alanına katılma de kullanabilirsiniz.
* **Azure AD dizini başına tek bir etki alanı örnek:** her Azure AD dizini için tek bir Active Directory etki alanı oluşturabilirsiniz.
* **Özel adlara sahip etki alanları oluşturun:** özel adları (örneğin, ' contoso100.com') olan Azure AD Etki Alanı Hizmetleri'ni kullanarak etki alanları oluşturabilirsiniz. Her iki doğrulanmış veya doğrulanmamış etki alanı adlarını kullanabilirsiniz. İsteğe bağlı olarak, aynı zamanda bir etki alanı hello yerleşik etki alanı sonekiyle oluşturabilirsiniz (diğer bir deyişle, ' *. onmicrosoft.com') Azure AD dizininizi tarafından sunulan.
* **Azure AD ile tümleşik:** , etmeyin tooconfigure gerekir veya çoğaltmayı yönetmek tooAzure AD etki alanı Hizmetleri. Kullanıcı hesapları, grup üyelikleri ve kullanıcı kimlik bilgilerini (Parolalar) Azure AD dizininizi Azure AD Etki Alanı Hizmetleri'nde otomatik olarak kullanılabilir. Yeni kullanıcılar, gruplar veya Azure AD kiracınıza veya şirket içi dizininize değişiklikleri tooattributes otomatik olarak eşitlenen tooAzure AD etki alanı Hizmetleri olabilir.
* **NTLM ve Kerberos kimlik doğrulaması:** NTLM ve Kerberos kimlik doğrulaması için desteği, Windows tümleşik kimlik doğrulamasını kullanan uygulamalar dağıtabilirsiniz.
* **Kurumsal kimlik bilgileri/parolalarınızı kullanın:** kullanıcıların Azure ad parolalarını Azure AD etki alanı Hizmetleri ile iş Kiracı. Kullanıcıların şirket kimlik bilgilerini toodomain birleştirme makinelerinin kullanın, etkileşimli olarak veya Uzak Masaüstü üzerinden oturum açın ve hello yönetilen etki alanına göre kimlik doğrulaması.
* **LDAP bağ & LDAP okuma desteği:** LDAP bağlamalar üzerinde Azure AD etki alanı Hizmetleri tarafından hizmet verilen etki alanlarındaki tooauthenticate kullanıcıları kullanan uygulamalar kullanabilirsiniz. Ayrıca, LDAP kullanan uygulamalar okuma işlemlerini tooquery kullanıcı/bilgisayar öznitelikleri hello dizininden ayrıca Azure AD Etki Alanı Hizmetleri'ne karşı çalışabilirsiniz.
* **Güvenli LDAP (LDAPS):** erişim toohello dizin güvenli LDAP (LDAPS üzerinden) etkinleştirebilirsiniz. Güvenli LDAP erişim varsayılan olarak hello sanal ağ içinde kullanılabilir. Ancak, ayrıca isteğe bağlı olarak güvenli LDAP erişimi hello etkinleştirebilir Internet.
* **Grup İlkesi:** hello kullanıcılar ve bilgisayarlar için tek bir yerleşik GPO'yu her kullanabileceğiniz kullanıcı hesapları ve etki alanına katılmış bilgisayarlar için gerekli güvenlik ilkeleriyle kapsayıcıları tooenforce uyumluluğu. Ayrıca kendi özel GPO'ları oluşturmak ve bunları toocustom kuruluş birimleri çok atayın[grup ilkesini yönetmenize](active-directory-ds-admin-guide-administer-group-policy.md).
* **DNS yönetme:** hello 'AAD DC Yöneticiler' grubunun üyeleri, DNS yönetebilir, bilinen DNS yönetimini kullanarak yönetilen etki alanınızın DNS Yönetim MMC ek bileşenini hello gibi araçları.
* **Özel Kuruluş birimlerini (OU) oluşturun:** hello 'AAD DC Yöneticiler' grubunun üyeleri hello yönetilen etki alanında özel OU'ları oluşturabilirsiniz. Bunlar Ekle/Kaldır böylece hizmet hesaplarını, bilgisayarlar, grupların vb. Bu özel OU içinde bu kullanıcıların özel OU'ları üzerinde tam yönetimsel ayrıcalıklara verilir.
* **Birden çok Azure bölgelerinde kullanılabilir:** bkz: Merhaba [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services/) sayfa tooknow hello Azure bölgeleri Azure AD etki alanı Hizmetleri olduğu kullanılabilir.
* **Yüksek Kullanılabilirlik:** Azure AD etki alanı Hizmetleri etki alanınız için yüksek kullanılabilirlik sağlar. Bu özellik yüksek hizmeti çalışır durumda kalma süresi ve esnekliği toofailures hello garanti sunar. Yerleşik durum dönen yeni örnekleri başarısız tooreplace örnekleri ve tooprovide tarafından teklifleri otomatik düzeltme hatalardan izleme hizmeti, etki alanınız için devam.
* **Tanıdık yönetim araçlarını kullanın:** hello Active Directory Yönetim Merkezi'ni veya Active Directory PowerShell tooadminister yönetilen etki alanı gibi bilinen Windows Server Active Directory yönetim araçlarını kullanabilirsiniz.
