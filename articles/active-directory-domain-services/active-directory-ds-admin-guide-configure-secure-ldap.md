---
title: "Güvenli LDAP (LDAPS) Azure AD Etki Alanı Hizmetleri'nde aaaConfigure | Microsoft Docs"
description: "Güvenli LDAP (LDAPS) bir Azure AD etki alanı Hizmetleri yönetilen etki alanını yapılandırın"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Güvenli LDAP (LDAPS) Azure AD etki alanı Hizmetleri yönetilen etki alanı için yapılandırma
Bu makalede, Azure AD etki alanı Hizmetleri yönetilen etki alanınız için Güvenli Basit Dizin Erişim Protokolü (LDAPS) nasıl etkinleştirebilirsiniz gösterilmektedir. Güvenli LDAP olduğu olarak da bilinen ' Basit Dizin Erişim Protokolü (LDAP) Güvenli Yuva Katmanı (SSL) üzerinden / Aktarım Katmanı Güvenliği (TLS)'.

## <a name="before-you-begin"></a>Başlamadan önce
Bu makalede listelenen tooperform hello görevleri, aşağıdakiler gerekir:

1. Geçerli bir **Azure aboneliği**.
2. Bir **Azure AD dizini** -ya da bir şirket içi dizin veya bir yalnızca bulut dizini ile eşitlenir.
3. **Azure AD etki alanı Hizmetleri** hello Azure AD dizini için etkinleştirilmesi gerekir. Bunu yapmadıysanız, hello özetlenen tüm hello görevleri izleyin [Getting Started guide](active-directory-ds-getting-started.md).
4. A **sertifika kullanılan toobe tooenable güvenli LDAP**.

   * **Önerilen** -bir güvenilir bir ortak sertifika yetkilisinden bir sertifika edinin. Bu yapılandırma seçeneği daha güvenlidir.
   * Alternatif olarak, ayrıca çok tercih[otomatik olarak imzalanan sertifika oluşturma](#task-1---obtain-a-certificate-for-secure-ldap) bu makalenin sonraki bölümlerinde gösterildiği gibi.

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a>Merhaba güvenli LDAP sertifika için gereksinimler
Güvenli LDAP etkinleştirmeden önce yönergeleri izleyerek hello başına geçerli bir sertifika edinin. Tooenable çalışırsanız hatalarıyla karşılaşırsanız geçersiz/hatalı bir sertifika ile yönetilen etki alanınız için LDAP güvenli.

1. **Güvenilen veren** -hello sertifikayı veren, güvenli LDAP kullanarak toohello yönetilen etki alanına bağlanan bilgisayarlar tarafından güvenilen bir yetkili tarafından. Bu yetkilisi bu bilgisayarlar tarafından güvenilen bir genel sertifika yetkilisinin olabilir.
2. **Yaşam süresi** -hello sertifika için geçerli olmalıdır en azından, sonraki 3-6 ay hello. Merhaba sertifikasının süresi sona erdiğinde güvenli LDAP erişim tooyour yönetilen etki alanı bozulur.
3. **Konu adı** -hello hello sertifika üzerindeki konu adı, yönetilen etki alanınız için joker karakter olmalıdır. Örneğin, etki alanınızın 'contoso100.com' adlı hello sertifikanın konu adı olması gerekir ' *. contoso100.com'. Merhaba DNS adı (konu alternatif adı) toothis joker adı ayarlayın.
4. **Anahtar kullanımı** - hello sertifika yapılandırılmalıdır aşağıdaki hello kullanan - dijital imzalar ve anahtar şifreleme.
5. **Sertifika amacı** -hello sertifika SSL sunucu kimlik doğrulaması için geçerli olmalıdır.

> [!NOTE]
> **Kuruluş sertifika yetkilileri:** Azure AD etki alanı Hizmetleri, kuruluşunuzun Kurumsal Sertifika yetkilisi tarafından verilen güvenli LDAP sertifikaları kullanarak desteklemez. Bu kısıtlama, Hello hizmet kuruluş kök sertifika yetkilisi olarak CA'nız güvenmezse olmasıdır. 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a>Görev 1 - güvenli LDAP için bir sertifika edinin
Güvenli LDAP erişim toohello yönetilen etki alanı için kullanılan bir sertifika edinme Hello ilk görev içerir. İki seçeneğiniz vardır:

* Bir sertifika yetkilisinden bir sertifika edinin. Merhaba yetkilisi, bir ortak sertifika yetkilisi olabilir.
* Kendinden imzalı bir sertifika oluşturun.

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a>(Önerilen). seçenek - bir sertifika yetkilisinden bir güvenli LDAP sertifikası alın
Kuruluşunuz bir ortak sertifika yetkilisi sertifikalarını alırsa, tooobtain hello güvenli LDAP sertifika konusu ortak sertifika yetkilisinden gerekir.

Sertifika isterken özetlenen tüm hello gereksinimleri karşılamak olun [hello güvenli LDAP sertifika için gereksinimler](#requirements-for-the-secure-ldap-certificate).

> [!NOTE]
> Güvenli LDAP kullanarak tooconnect toohello yönetilen etki alanına ihtiyacınız istemci bilgisayarlarının hello güvenli LDAP sertifikayı hello veren güvenmesi gerekir.
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a>Seçeneği B - güvenli LDAP için otomatik olarak imzalanan sertifika oluşturma
Bir ortak sertifika yetkilisinden bir sertifika toouse düşünmüyorsanız toocreate güvenli LDAP için otomatik olarak imzalanan bir sertifika tercih edebilirsiniz.

**PowerShell kullanarak otomatik olarak imzalanan bir sertifika oluşturun**

Windows bilgisayarınızda olarak yeni bir PowerShell penceresi açın **yönetici** ve türü hello aşağıdaki komutlar, toocreate yeni bir otomatik olarak imzalanan sertifika.

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

Örnek önceki hello Değiştir '*. contoso100.com' hello DNS etki alanı adı, yönetilen etki alanınızın. 'Contoso100.onmicrosoft.com' adında yönetilen bir etki alanı oluşturduysanız, for example, Değiştir '*. contoso100.com' hello komut dosyasıyla yukarıda içinde ' *. contoso100.onmicrosoft.com').

![Azure AD Dizini Seçme](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

Yeni oluşturulan hello otomatik olarak imzalanan sertifika hello yerel makinenin sertifika deposuna yerleştirilir.


## <a name="next-step"></a>Sonraki adım
[Görev 2 - hello güvenli LDAP sertifika tooa dışarı aktarma. PFX dosyası](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
