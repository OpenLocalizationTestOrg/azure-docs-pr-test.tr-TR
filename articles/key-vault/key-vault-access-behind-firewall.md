---
title: "bir güvenlik duvarının arkasında aaaAccess anahtar kasası | Microsoft Docs"
description: "Tooaccess Azure anahtar kasası nasıl bir güvenlik duvarının arkasında uygulamadan öğrenin"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: ab4bb0c27a41fef878a20dace6cab203df04e579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>Güvenlik duvarının ardındayken Azure Anahtar Kasası’na erişme
### <a name="q-my-key-vault-client-application-needs-toobe-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-tooenable-access-tooa-key-vault"></a>S: my anahtar kasası istemci uygulamasının bir güvenlik duvarının arkasında toobe gerekiyor. Hangi bağlantı noktaları, ana bilgisayar veya IP adresleri tooenable erişim tooa anahtar kasası açmanız gerekir?
tooaccess bir anahtar kasası, anahtar kasası istemci uygulamanızı tooaccess çeşitli işlevler için birden çok uç noktalar vardır:

* Azure Active Directory aracılığıyla kimlik doğrulama (Azure AD).
* Azure Anahtar Kasası'nın yönetimi. Buna, Azure Resource Manager aracılığıyla erişim ilkeleri oluşturma, okuma, güncelleştirme, silme ve ayarlama da dahildir.
* Erişme ve kendisini anahtar kasasında depolanan nesneler (anahtarları ve gizli anahtarları) yönetme, anahtar kasası özgü endpoint hello oluşturulmak (örneğin, [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).  

Yapılandırmanıza ve ortamınıza bağlı olarak, bazı farklılıklar mevcuttur.   

## <a name="ports"></a>Bağlantı Noktaları
Tüm trafiği tooa anahtar kasası tüm üç işlevleri (kimlik doğrulaması, yönetim ve veri düzlemi erişimi) için HTTPS üzerinden gider: bağlantı noktası 443'tür. Ancak CRL için zaman zaman HTTP (bağlantı noktası 80) trafiği de olacaktır. OCSP destekleyen istemciler CRL'ye erişmemelidir, ancak zaman zaman [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl)'ye erişebilirler.  

## <a name="authentication"></a>Kimlik Doğrulaması
Anahtar kasası istemci uygulamaları tooaccess Azure Active Directory uç noktaları için kimlik doğrulaması gerekir. kullanılan hello endpoint hello üzerinde Azure AD Kiracı yapılandırmasına bağlıdır, hello türünü sorumlusu (kullanıcı asıl ya da hizmet sorumlusu) ve hello hesabı--Örneğin, bir Microsoft hesabı veya bir iş yazın veya Okul hesabı.  

| Sorumlu türü | Uç nokta:bağlantı noktası |
| --- | --- |
| Microsoft hesabı kullanan kullanıcı<br> (örneğin, user@hotmail.com) |**Genel:**<br> login.microsoftonline.com:443<br><br> **Azure Çin:**<br> login.chinacloudapi.cn:443<br><br>**Azure ABD:**<br> login-us.microsoftonline.com:443<br><br>**Azure Almanya:**<br> login.microsoftonline.de:443<br><br> ve <br>login.live.com:443 |
| Kullanıcı veya Azure AD ile bir iş veya Okul hesabı kullanarak hizmet sorumlusu (örneğin, user@contoso.com) |**Genel:**<br> login.microsoftonline.com:443<br><br> **Azure Çin:**<br> login.chinacloudapi.cn:443<br><br>**Azure ABD:**<br> login-us.microsoftonline.com:443<br><br>**Azure Almanya:**<br> login.microsoftonline.de:443 |
| Kullanıcı veya bir iş veya Okul hesabı yanı sıra Active Directory Federasyon Hizmetleri (AD FS) veya Federasyon diğer uç nokta kullanarak hizmet sorumlusu (örneğin, user@contoso.com) |İş veya okul hesabı için tüm uç noktalar ve AD FS veya diğer federasyon uç noktaları |

Farklı olası karmaşık senaryolar da mevcuttur. Çok başvuran[Azure Active Directory kimlik doğrulama akışı](/documentation/articles/active-directory-authentication-scenarios/), [Azure Active Directory Tümleştirme uygulamalarla](/documentation/articles/active-directory-integrating-applications/), ve [Active Directory kimlik doğrulama protokolleri](https://msdn.microsoft.com/library/azure/dn151124.aspx) ek bilgi için.  

## <a name="key-vault-management"></a>Anahtar Kasası yönetimi
Anahtar kasası Yönetim (CRUD ve erişim ilkesi ayarını), tooaccess bir Azure Resource Manager uç nokta Merhaba anahtar kasası istemci uygulaması gerekir.  

| İşlem türü | Uç nokta:bağlantı noktası |
| --- | --- |
| Anahtar Kasası denetim düzlemi işlemleri<br> Azure Resource Manager yoluyla |**Genel:**<br> management.azure.com:443<br><br> **Azure Çin:**<br> management.chinacloudapi.cn:443<br><br> **Azure ABD:**<br> management.usgovcloudapi.net:443<br><br> **Azure Almanya:**<br> management.microsoftazure.de:443 |
| Azure Active Directory Grafik API'si |**Genel:**<br> graph.windows.net:443<br><br> **Azure Çin:**<br> graph.chinacloudapi.cn:443<br><br> **Azure ABD:**<br> graph.windows.net:443<br><br> **Azure Almanya:**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>Anahtar Kasası işlemleri
Tüm anahtar kasası nesne (anahtarları ve gizli anahtarları) yönetimi ve şifreleme işlemleri için hello anahtar kasası istemci tooaccess hello anahtar kasası endpoint gerekir. Merhaba uç noktası DNS soneki anahtar kasanızı hello konuma bağlı olarak değişir. Merhaba anahtar kasası uç noktadır hello biçimi *kasa adı*. *Bölge özel dns soneki*, aşağıdaki tablonun hello açıklandığı gibi.  

| İşlem türü | Uç nokta:bağlantı noktası |
| --- | --- |
| Anahtarlar üzerindeki şifreleme işlemlerini de içeren işlemler, anahtarları ve gizli anahtarları oluşturma, okuma, güncelleştirme ve silme, anahtar kasası nesnelerindeki etiketleri ve diğer öznitelikleri (anahtarlar ya da gizli anahtarlar) ayarlama veya alma |**Genel:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure Çin:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure ABD:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Almanya:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>IP adresi aralıkları
Merhaba anahtar kasası hizmetindeki PaaS altyapı gibi diğer Azure kaynaklarını kullanır. Olası tooprovide değil sağlayacak şekilde belirli bir zamanda hizmet uç noktalarına sahip olur, anahtar kasası belirli IP adreslerini. Güvenlik duvarını yalnızca IP adres aralıklarını destekliyorsa, toohello başvuran [Microsoft Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653) belge. Kimlik doğrulama ve kimlik (Azure Active Directory) için uygulamanızın mümkün tooconnect toohello uç noktaları açıklanan olmalıdır [kimlik doğrulama ve kimlik adresleri](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="next-steps"></a>Sonraki adımlar
Anahtar kasası hakkında sorularınız varsa hello ziyaret [Azure anahtar kasası forumları](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

