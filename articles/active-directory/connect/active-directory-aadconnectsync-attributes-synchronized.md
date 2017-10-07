---
title: "Öznitelikleri eşitlenmiş Azure AD Connect tarafından | Microsoft Docs"
description: "Listeleri hello öznitelikleri tooAzure Active Directory eşitlendi."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 2fe5b944a7fc832f245631416c265fb82eedeb15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-attributes-synchronized-tooazure-active-directory"></a>Azure AD Connect eşitleme: öznitelikleri eşitlenir tooAzure Active Directory
Bu konuda, Azure AD Connect eşitleme tarafından eşitlenen hello öznitelikleri listeler.  
Merhaba öznitelikleri ilgili hello göre gruplandırılır Azure AD uygulaması.

## <a name="attributes-toosynchronize"></a>Öznitelikleri toosynchronize
Ortak bir soru *düşük öznitelikler toosynchronize hello listesi nedir*. Merhaba varsayılan ve önerilen yaklaşım olan tam GAL (genel adres listesi) içinde yapılandırılan şekilde tookeep hello varsayılan öznitelikleri Bulut ve tooget Office 365 iş yükleri'ındaki tüm özelliklere hello. Bazı durumlarda, bu öznitelikler içeren bu yana kuruluşunuz eşitlenmiş toohello bulut hassas istemediği bazı öznitelikler vardır veya PII (kişisel bilgi) verileri, bu örnekte, ister:  
![hatalı öznitelikleri](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

Bu durumda, bu konu içinde öznitelik listesi hello başlayın ve duyarlı veya PII veri içerir ve eşitlenemiyor özniteliklerle tanımlayın. Ardından yükleme kullanarak sırasında özniteliklerle seçimini [Azure AD uygulaması ve öznitelik filtrelemesi](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering).

> [!WARNING]
> Öznitelikleri seçimini zaman dikkatli olun ve yalnızca bu öznitelikler yapılamaz kesinlikle toosynchronize seçimini kaldırın. Diğer öznitelikleri unselecting özellikleri olumsuz bir etkisi olabilir.
>
>

## <a name="office-365-proplus"></a>Office 365 ProPlus
| Öznitelik adı | Kullanıcı | Açıklama |
| --- |:---:| --- |
| accountEnabled |X |Bir hesap etkinleştirilirse tanımlar. |
| CN = |X | |
| Görünen adı |X | |
| objectSID |X |mekanik özelliği. AD Kullanıcı tanımlayıcısı toomaintain eşitleme Azure arasında kullanılan AD ve AD. |
| pwdLastSet |X |mekanik özelliği. Tooinvalidate zaten verilen belirteçler zaman kullanılan tooknow. Parola Eşitleme ve Federasyon tarafından kullanılır. |
| sourceAnchor |X |mekanik özelliği. EKLER ve Azure AD arasındaki değişmez tanımlayıcı toomaintain ilişki. |
| usageLocation |X |mekanik özelliği. Merhaba kullanıcının ülke. Lisans atama için kullanılır. |
| userPrincipalName |X |UPN hello oturum açma hello kullanıcı kimliğidir. En sık [posta] değeri olarak aynı hello. |

## <a name="exchange-online"></a>Exchange Online
| Öznitelik adı | Kullanıcı | İletişim | Grup | Açıklama |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Bir hesap etkinleştirilirse tanımlar. |
| Yardımcısı |X |X | | |
| altRecipient |X | | |Azure AD Connect yapı 1.1.552.0 gerektirir veya sonra. |
| authOrig |X |X |X | |
| C |X |X | | |
| CN = |X | |X | |
| Ortak |X |X | | |
| Şirket |X |X | | |
| CountryCode |X |X | | |
| Bölüm |X |X | | |
| açıklama |X |X |X | |
| Görünen adı |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| HomePhone |X |X | | |
| bilgileri |X |X |X |Bu özellik şu anda grupları için kullanılmaz. |
| baş harfleri |X |X | | |
| m |X |X | | |
| LegacyExchangeDN |X |X |X | |
| mailNickname |X |X |X | |
| mangedBy | | |X | |
| Yöneticisi |X |X | | |
| Üye | | |X | |
| Mobil |X |X | | |
| msDS-HABSeniorityIndex |X |X |X | |
| msDS-PhoneticDisplayName |X |X |X | |
| msExchArchiveGUID |X | | | |
| msExchArchiveName |X | | | |
| değerlerinin msExchAssistantName |X |X | | |
| msExchAuditAdmin |X | | | |
| msExchAuditDelegate |X | | | |
| msExchAuditDelegateAdmin |X | | | |
| msExchAuditOwner |X | | | |
| msExchBlockedSendersHash |X |X | | |
| msExchBypassAudit |X | | | |
| msExchBypassModerationLink | | |X |Azure AD CONNECT'te sürüm 1.1.524.0 kullanılabilir |
| msExchCoManagedByLink | | |X | |
| msExchDelegateListLink |X | | | |
| msExchELCExpirySuspensionEnd |X | | | |
| msExchELCExpirySuspensionStart |X | | | |
| msExchELCMailboxFlags |X | | | |
| msExchEnableModeration |X | |X | |
| msExchExtensionCustomAttribute1 |X |X |X |Bu özellik şu anda Exchange Online tarafından mı tüketiliyor değil. |
| msExchExtensionCustomAttribute2 |X |X |X |Bu özellik şu anda Exchange Online tarafından mı tüketiliyor değil. |
| msExchExtensionCustomAttribute3 |X |X |X |Bu özellik şu anda Exchange Online tarafından mı tüketiliyor değil. |
| msExchExtensionCustomAttribute4 |X |X |X |Bu özellik şu anda Exchange Online tarafından mı tüketiliyor değil. |
| msExchExtensionCustomAttribute5 |X |X |X |Bu özellik şu anda Exchange Online tarafından mı tüketiliyor değil. |
| msExchHideFromAddressLists |X |X |X | |
| msExchImmutableID |X | | | |
| msExchLitigationHoldDate |X |X |X | |
| msExchLitigationHoldOwner |X |X |X | |
| msExchMailboxAuditEnable |X | | | |
| msExchMailboxAuditLogAgeLimit |X | | | |
| msExchMailboxGUID |X | | | |
| msExchModeratedByLink |X |X |X | |
| msExchModerationFlags |X |X |X | |
| msExchRecipientDisplayType |X |X |X | |
| msExchRecipientTypeDetails |X |X |X | |
| msExchRemoteRecipientType |X | | | |
| msExchRequireAuthToSendTo |X |X |X | |
| msExchResourceCapacity |X | | | |
| msExchResourceDisplay |X | | | |
| msExchResourceMetaData |X | | | |
| msExchResourceSearchProperties |X | | | |
| msExchRetentionComment |X |X |X | |
| msExchRetentionURL |X |X |X | |
| msExchSafeRecipientsHash |X |X | | |
| msExchSafeSendersHash |X |X | | |
| msExchSenderHintTranslations |X |X |X | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| msExchUserHoldPolicies |X | | | |
| msOrg IsOrganizational | | |X | |
| objectSID |X | |X |mekanik özelliği. AD Kullanıcı tanımlayıcısı toomaintain eşitleme Azure arasında kullanılan AD ve AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| Çağrı cihazı |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| posta kodu |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |mekanik özelliği. Tooinvalidate zaten verilen belirteçler zaman kullanılan tooknow. Parola Eşitleme ve Federasyon tarafından kullanılır. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |GroupType türetilmiş |
| sn |X |X | | |
| sourceAnchor |X |X |X |mekanik özelliği. EKLER ve Azure AD arasındaki değişmez tanımlayıcı toomaintain ilişki. |
| St |X |X | | |
| StreetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| Başlık |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |mekanik özelliği. Merhaba kullanıcının ülke. Lisans atama için kullanılır. |
| userCertificate |X |X | | |
| userPrincipalName |X | | |UPN hello oturum açma hello kullanıcı kimliğidir. En sık [posta] değeri olarak aynı hello. |
| userSMIMECertificates |X |X | | |
| wWWHomePage |X |X | | |

## <a name="sharepoint-online"></a>SharePoint Online
| Öznitelik adı | Kullanıcı | İletişim | Grup | Açıklama |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Bir hesap etkinleştirilirse tanımlar. |
| authOrig |X |X |X | |
| C |X |X | | |
| CN = |X | |X | |
| Ortak |X |X | | |
| Şirket |X |X | | |
| CountryCode |X |X | | |
| Bölüm |X |X | | |
| açıklama |X |X |X | |
| Görünen adı |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| hideDLMembership | | |X | |
| homephone |X |X | | |
| bilgileri |X |X |X | |
| baş harfleri |X |X | | |
| ipPhone |X |X | | |
| m |X |X | | |
| Posta |X |X |X | |
| mailnickname |X |X |X | |
| Şirketiniz tarafından | | |X | |
| Yöneticisi |X |X | | |
| Üye | | |X | |
| middleName |X |X | | |
| Mobil |X |X | | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointLinkedBy |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| objectSID |X | |X |mekanik özelliği. AD Kullanıcı tanımlayıcısı toomaintain eşitleme Azure arasında kullanılan AD ve AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherIpPhone |X |X | | |
| OtherMobile |X |X | | |
| otherPager |X |X | | |
| otherTelephone |X |X | | |
| Çağrı cihazı |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| posta kodu |X |X | | |
| postOfficeBox |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |mekanik özelliği. Tooinvalidate zaten verilen belirteçler zaman kullanılan tooknow. Parola Eşitleme ve Federasyon tarafından kullanılır. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |GroupType türetilmiş |
| sn |X |X | | |
| sourceAnchor |X |X |X |mekanik özelliği. EKLER ve Azure AD arasındaki değişmez tanımlayıcı toomaintain ilişki. |
| St |X |X | | |
| StreetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| Başlık |X |X | | |
| unauthOrig |X |X |X | |
| URL |X |X | | |
| usageLocation |X | | |mekanik özelliği. Merhaba kullanıcının ülke. Lisans atama için kullanılır. |
| userPrincipalName |X | | |UPN hello oturum açma hello kullanıcı kimliğidir. En sık [posta] değeri olarak aynı hello. |
| wWWHomePage |X |X | | |

## <a name="lync-online"></a>Lync Online
| Öznitelik adı | Kullanıcı | İletişim | Grup | Açıklama |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Bir hesap etkinleştirilirse tanımlar. |
| C |X |X | | |
| CN = |X | |X | |
| Ortak |X |X | | |
| Şirket |X |X | | |
| Bölüm |X |X | | |
| açıklama |X |X |X | |
| Görünen adı |X |X |X | |
| facsimiletelephonenumber |X |X |X | |
| givenName |X |X | | |
| homephone |X |X | | |
| ipPhone |X |X | | |
| m |X |X | | |
| Posta |X |X |X | |
| mailNickname |X |X |X | |
| Şirketiniz tarafından | | |X | |
| Yöneticisi |X |X | | |
| Üye | | |X | |
| Mobil |X |X | | |
| msExchHideFromAddressLists |X |X |X | |
| Msrtcsıp-ApplicationOptions |X | | | |
| Msrtcsıp-DeploymentLocator |X |X | | |
| Msrtcsıp-Line |X |X | | |
| Msrtcsıp-OptionFlags |X |X | | |
| Msrtcsıp-OwnerUrn |X | | | |
| Msrtcsıp-Primaryuseraddress'teki |X |X | | |
| Msrtcsıp-UserEnabled |X |X | | |
| objectSID |X | |X |mekanik özelliği. AD Kullanıcı tanımlayıcısı toomaintain eşitleme Azure arasında kullanılan AD ve AD. |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| posta kodu |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |mekanik özelliği. Tooinvalidate zaten verilen belirteçler zaman kullanılan tooknow. Parola Eşitleme ve Federasyon tarafından kullanılır. |
| securityEnabled | | |X |GroupType türetilmiş |
| sn |X |X | | |
| sourceAnchor |X |X |X |mekanik özelliği. EKLER ve Azure AD arasındaki değişmez tanımlayıcı toomaintain ilişki. |
| St |X |X | | |
| StreetAddress |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| Başlık |X |X | | |
| usageLocation |X | | |mekanik özelliği. Merhaba kullanıcının ülke. Lisans atama için kullanılır. |
| userPrincipalName |X | | |UPN hello oturum açma hello kullanıcı kimliğidir. En sık [posta] değeri olarak aynı hello. |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>Azure RMS
| Öznitelik adı | Kullanıcı | İletişim | Grup | Açıklama |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Bir hesap etkinleştirilirse tanımlar. |
| CN = |X | |X |Ortak adı veya diğer ad. En sık hello öneki [posta] değeri. |
| Görünen adı |X |X |X |Genellikle hello kolay ad (ad Soyadı) olarak gösterilen hello adını temsil eden bir dize. |
| Posta |X |X |X |tam e-posta adresi. |
| Üye | | |X | |
| objectSID |X | |X |mekanik özelliği. AD Kullanıcı tanımlayıcısı toomaintain eşitleme Azure arasında kullanılan AD ve AD. |
| proxyAddresses |X |X |X |mekanik özelliği. Azure AD tarafından kullanılır. Merhaba kullanıcı için tüm ikincil e-posta adreslerini içerir. |
| pwdLastSet |X | | |mekanik özelliği. Tooinvalidate zaten verilen belirteçler zaman kullanılan tooknow. |
| securityEnabled | | |X |GroupType türetilmiş. |
| sourceAnchor |X |X |X |mekanik özelliği. EKLER ve Azure AD arasındaki değişmez tanımlayıcı toomaintain ilişki. |
| usageLocation |X | | |mekanik özelliği. Merhaba kullanıcının ülke. Lisans atama için kullanılır. |
| userPrincipalName |X | | |Bu UPN hello oturum açma hello kullanıcı kimliğidir. En sık [posta] değeri olarak aynı hello. |

## <a name="intune"></a>Intune
| Öznitelik adı | Kullanıcı | İletişim | Grup | Açıklama |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Bir hesap etkinleştirilirse tanımlar. |
| C |X |X | | |
| CN = |X | |X | |
| açıklama |X |X |X | |
| Görünen adı |X |X |X | |
| Posta |X |X |X | |
| mailnickname |X |X |X | |
| Üye | | |X | |
| objectSID |X | |X |mekanik özelliği. AD Kullanıcı tanımlayıcısı toomaintain eşitleme Azure arasında kullanılan AD ve AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |mekanik özelliği. Tooinvalidate zaten verilen belirteçler zaman kullanılan tooknow. Parola Eşitleme ve Federasyon tarafından kullanılır. |
| securityEnabled | | |X |GroupType türetilmiş |
| sourceAnchor |X |X |X |mekanik özelliği. EKLER ve Azure AD arasındaki değişmez tanımlayıcı toomaintain ilişki. |
| usageLocation |X | | |mekanik özelliği. Merhaba kullanıcının ülke. Lisans atama için kullanılır. |
| userPrincipalName |X | | |UPN hello oturum açma hello kullanıcı kimliğidir. En sık [posta] değeri olarak aynı hello. |

## <a name="dynamics-crm"></a>Dynamics CRM
| Öznitelik adı | Kullanıcı | İletişim | Grup | Açıklama |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Bir hesap etkinleştirilirse tanımlar. |
| C |X |X | | |
| CN = |X | |X | |
| Ortak |X |X | | |
| Şirket |X |X | | |
| CountryCode |X |X | | |
| açıklama |X |X |X | |
| Görünen adı |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| m |X |X | | |
| Şirketiniz tarafından | | |X | |
| Yöneticisi |X |X | | |
| Üye | | |X | |
| Mobil |X |X | | |
| objectSID |X | |X |mekanik özelliği. AD Kullanıcı tanımlayıcısı toomaintain eşitleme Azure arasında kullanılan AD ve AD. |
| physicalDeliveryOfficeName |X |X | | |
| posta kodu |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |mekanik özelliği. Tooinvalidate zaten verilen belirteçler zaman kullanılan tooknow. Parola Eşitleme ve Federasyon tarafından kullanılır. |
| securityEnabled | | |X |GroupType türetilmiş |
| sn |X |X | | |
| sourceAnchor |X |X |X |mekanik özelliği. EKLER ve Azure AD arasındaki değişmez tanımlayıcı toomaintain ilişki. |
| St |X |X | | |
| StreetAddress |X |X | | |
| telephoneNumber |X |X | | |
| Başlık |X |X | | |
| usageLocation |X | | |mekanik özelliği. Merhaba kullanıcının ülke. Lisans atama için kullanılır. |
| userPrincipalName |X | | |UPN hello oturum açma hello kullanıcı kimliğidir. En sık [posta] değeri olarak aynı hello. |

## <a name="3rd-party-applications"></a>3 taraf uygulamalar
Bu grup, genel iş yükü veya uygulama için gerekli en az öznitelikleri hello olarak kullanılan öznitelikler kümesidir. Microsoft olmayan uygulama veya başka bir bölümünde listelenmeyen bir iş yükü için kullanılabilir. Açıkça hello şunlar için de kullanılır:

* (Yalnızca kullanıcı tüketilen) yammer
* [SharePoint gibi kaynaklar tarafından sunulan karma işletmeden işletmeye (B2B) org arası işbirliği senaryoları](http://go.microsoft.com/fwlink/?LinkId=747036)

Bu grubun bir hello Azure AD dizini değilse, kullanılabilen öznitelikler kümesi toosupport Office 365, Dynamics ya da Intune kullanılır. Küçük bir çekirdek öznitelikler kümesi vardır.

| Öznitelik adı | Kullanıcı | İletişim | Grup | Açıklama |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Bir hesap etkinleştirilirse tanımlar. |
| CN = |X | |X | |
| Görünen adı |X |X |X | |
| givenName |X |X | | |
| Posta |X | |X | |
| Şirketiniz tarafından | | |X | |
| mailNickName |X |X |X | |
| Üye | | |X | |
| objectSID |X | | |mekanik özelliği. AD Kullanıcı tanımlayıcısı toomaintain eşitleme Azure arasında kullanılan AD ve AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |mekanik özelliği. Tooinvalidate zaten verilen belirteçler zaman kullanılan tooknow. Parola Eşitleme ve Federasyon tarafından kullanılır. |
| sn |X |X | | |
| sourceAnchor |X |X |X |mekanik özelliği. EKLER ve Azure AD arasındaki değişmez tanımlayıcı toomaintain ilişki. |
| usageLocation |X | | |mekanik özelliği. Merhaba kullanıcının ülke. Lisans atama için kullanılır. |
| userPrincipalName |X | | |UPN hello oturum açma hello kullanıcı kimliğidir. En sık [posta] değeri olarak aynı hello. |

## <a name="windows-10"></a>Windows 10
Etki alanına katılmış Windows 10 computer(device) bazı öznitelikler tooAzure AD eşitler. Merhaba senaryoları hakkında daha fazla bilgi için bkz: [Windows 10 deneyimleri için etki alanına katılmış aygıtlar tooAzure AD Connect](../active-directory-azureadjoin-devices-group-policy.md). Bu öznitelikler her zaman eşitleyin ve Windows 10 işaretini kaldırabilirsiniz bir uygulama görünmez. Windows 10 etki alanına katılmış bir bilgisayar doldurulmuş hello özniteliği userCertificate sahip olarak tanımlanır.

| Öznitelik adı | Cihaz | Açıklama |
| --- |:---:| --- |
| accountEnabled |X | |
| deviceTrustType |X |Etki alanına katılmış bilgisayarlar için sabit kodlu değeri. |
| Görünen adı |X | |
| MS DS CreatorSID |X |RegisteredOwnerReference olarak da bilinir. |
| objectGUID |X |Cihaz kimliği olarak da bilinir. |
| objectSID |X |OnPremisesSecurityIdentifier olarak da bilinir. |
| operatingSystem |X |DeviceOSType olarak da bilinir. |
| İşletimsistemisürümü |X |DeviceOSVersion olarak da bilinir. |
| userCertificate |X | |

Bu öznitelikler için **kullanıcı** ayrıca toohello seçtiğiniz diğer uygulamalardır.  

| Öznitelik adı | Kullanıcı | Açıklama |
| --- |:---:| --- |
| domainFQDN |X |DNSEtkiAlanıAdı olarak da bilinir. Örneğin, contoso.com. |
| domainNetBios |X |NetBiosName olarak da bilinir. Örneğin, CONTOSO. |

## <a name="exchange-hybrid-writeback"></a>Exchange karma geri yazma
Tooenable seçtiğinizde bu öznitelikler Azure AD tooon içi Active Directory geri yazılır **Exchange karma**. Exchange sürümünüzün bağlı olarak, daha az sayıda öznitelik eşitlenmiş olabilir.

| Öznitelik adı | Kullanıcı | İletişim | Grup | Açıklama |
| --- |:---:|:---:|:---:| --- |
| msDS-ExternalDirectoryObjectID |X | | |Azure AD'de cloudAnchor türetilmiş. Bu öznitelik, Exchange 2016 ve Windows Server 2016 AD yenidir. |
| msExchArchiveStatus |X | | |Çevrimiçi Arşiv: müşteriler tooarchive posta sağlar. |
| msExchBlockedSendersHash |X | | |Filtreleme: geri filtreleme şirket içi ve çevrimiçi güvenli ve Engellenen gönderen veri istemcilerden yazar. |
| msExchSafeRecipientsHash |X | | |Filtreleme: geri filtreleme şirket içi ve çevrimiçi güvenli ve Engellenen gönderen veri istemcilerden yazar. |
| msExchSafeSendersHash |X | | |Filtreleme: geri filtreleme şirket içi ve çevrimiçi güvenli ve Engellenen gönderen veri istemcilerden yazar. |
| msExchUCVoiceMailSettings |X | | |Birleşik Mesajlaşma (UM) - çevrimiçi sesli posta etkinleştirin: Microsoft Lync Server Tümleştirme tooindicate tooLync tarafından kullanılan şirket içi Server hello kullanıcının çevrimiçi hizmetlerinde sesli posta sahip. |
| msExchUserHoldPolicies |X | | |Mahkeme tutun: kullanıcıların mahkeme tutma altında olan bulut Hizmetleri toodetermine sağlar. |
| proxyAddresses |X |X |X |Yalnızca Exchange Online'dan hello x500 adresi eklenir. |
| publicDelegates |X | | |SendOnBehalfTo hakları toousers şirket içi Exchange posta kutusu ile bir Exchange Online posta kutusu toobe izni verir. Azure AD Connect yapı 1.1.552.0 gerektirir veya sonra. |

## <a name="exchange-mail-public-folder"></a>Exchange posta ortak klasörü
Bu öznitelikler şirket içi Active Directory tooAzure tooenable seçtiğinizde, AD eşitlenir **Exchange posta ortak klasör**.

| Öznitelik adı | PublicFolder | Açıklama |
| --- | :---:| --- |
| Görünen adı | X |  |
| Posta | X |  |
| msExchRecipientTypeDetails | X |  |
| objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>Cihaz geri yazma
Cihaz nesneleri, Active Directory içinde oluşturulur. Bu nesneler tooAzure AD veya etki alanına katılmış Windows 10 bilgisayarları katılmış cihazlarda olabilir.

| Öznitelik adı | Cihaz | Açıklama |
| --- |:---:| --- |
| altSecurityIdentities |X | |
| Görünen adı |X | |
| DN |X | |
| msDS-CloudAnchor |X | |
| msDS-DeviceID |X | |
| msDS-DeviceObjectVersion |X | |
| msDS-DeviceOSType |X | |
| msDS-DeviceOSVersion |X | |
| msDS-DevicePhysicalIDs |X | |
| msDS-KeyCredentialLink |X |Yalnızca Windows Server 2016 AD şemasıyla |
| msDS-IsCompliant |X | |
| msDS-IsEnabled |X | |
| msDS-Ismanaged |X | |
| msDS-RegisteredOwner |X | |

## <a name="notes"></a>Notlar
* Alternatif kimlik, hello kullanarak şirket içi zaman özniteliği userPrincipalName hello Azure AD özniteliği onPremisesUserPrincipalName ile eşitlenir. Alternatif kimlik öznitelik Merhaba, örneğin posta, hello Azure AD özniteliği userPrincipalName ile eşitlenir.
* Nesne türü Hello listelerinde yukarıdaki hello **kullanıcı** toohello nesne türü için de geçerlidir **iNetOrgPerson**.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
