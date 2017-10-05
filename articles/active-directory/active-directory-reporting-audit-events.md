---
title: "Azure Active Directory Denetim Raporu olayları | Microsoft Docs"
description: "Görüntüleme ve Azure Active Directory'den indirme için kullanılabilir olan olayları denetleniyor"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 307eedf7-05bc-448d-a84d-bead5a4c5770
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 1620d917acf5a2c36767b5b03750c405f3631ee2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Azure Active Directory denetim raporu olayları
*Bu belge, [Azure Active Directory Raporlama Kılavuzu](active-directory-reporting-guide.md)’nun bir parçasıdır.*

Azure Active Directory denetim raporu, müşterilerin kendi Azure Active Directory'de oluştu ayrıcalıklı Eylemler tanımlamak yardımcı olur. Ayrıcalıklı Eylemler ayrıcalık değişiklikler (örneğin, rolü oluşturma veya parola sıfırlama), değişen ilke yapılandırmaları (örneğin, parola ilkelerinin) veya dizin yapılandırması (örneğin, etki alanı Federasyon ayarlarında yapılan değişiklikler) değişiklikleri içerir. Raporlar, olay adı için değişiklik ve tarih ve saat (UTC) etkilenen hedef kaynak eylemi gerçekleştiren aktör denetim kaydını sağlar. Müşteriler kendi Azure Active Directory için denetim olayları listesini almak için [Azure Portal](https://portal.azure.com/)açıklandığı gibi [denetim günlüklerini görüntülemek](active-directory-reporting-azure-portal.md).

## <a name="list-of-audit-report-events"></a>Denetim Raporu olayları listesi
<!--- audit event descriptions should be in the past tense --->

| Olaylar | Olay açıklaması |
| --- | --- |
| **Kullanıcı olayları** | |
| Kullanıcı Ekleme |Kullanıcının dizine eklendi. |
| Kullanıcıyı Silme |Bir kullanıcı dizinden silinir. |
| Lisans özelliklerini ayarlama |Dizindeki bir kullanıcı için lisans özellikleri ayarlayın. |
| Kullanıcı parolasını sıfırlama |Dizindeki bir kullanıcı parolasını sıfırlayın. |
| Kullanıcı parolasını değiştirme |Dizindeki bir kullanıcı parolası değiştirildi. |
| Değişiklik kullanıcı lisansı |Dizindeki bir kullanıcıya atanan lisans değiştirildi. Hangi lisansları güncelleştirildi görmek için bakmak [güncelleştirme kullanıcı](#update-user-attributes) aşağıdaki özellikleri |
| Kullanıcıyı güncelleştirir |Dizindeki bir kullanıcı güncelleştirildi. [Aşağıya bakın](#update-user-attributes) güncelleştirilebilir öznitelikler için. |
| Kullanıcı parolasını değiştirme kümesi zorla |Bir kullanıcı oturum açma parolalarını değiştirmek için zorlar özelliğini ayarlayın. |
| Kullanıcı kimlik bilgilerini güncelleştir |Kullanıcı parolası değiştirildi |
| **Grup olayları** | |
| Grup Ekle |Bir grup dizinde oluşturuldu. |
| Güncelleştirme grubu |Dizinde bir grubu güncelleştirildi. Hangi Grup Özellikleri güncelleştirildi görmek için bkz [Grup Özellikleri denetlenen](#update-group-attributes) bölümünde |
| Grup silme |Bir grup dizinden silinir. |
| CreateGroupSettings |Oluşturulan Grup ayarları |
| UpdateGroupSettings |Grup ayarları güncelleştirildi. Hangi Grup ayarları güncelleştirildi görmek için bkz [Grup Özellikleri denetlenen](#update-group-attributes) bölümünde |
| DeleteGroupSettings |Silinen grup ayarları |
| SetGroupLicense |Grup lisans ayarlayın. |
| SetGroupManagedBy |Kullanıcı tarafından yönetilecek grubunu Ayarla |
| AddGroupMember |Gruba eklenen üye |
| RemoveGroupMember |Grubundan üye kaldırma |
| AddGroupOwner |Gruba eklenen sahibi |
| RemoveGroupOwner |Gruptan kaldırılan sahibi |
| **Uygulama olayları** | |
| Hizmet sorumlusu ekleme |Bir hizmet sorumlusu dizine eklendi. |
| Hizmet sorumlusu Kaldır |Bir hizmet sorumlusu dizinden kaldırıldı. |
| Hizmet asıl kimlik bilgileri ekleme |Bir hizmet asıl için kimlik bilgileri eklendi. |
| Hizmet asıl kimlik bilgilerini kaldırma |Bir hizmet sorumlusu kaldırılan kimlik bilgileri. |
| Temsilci Girişi Ekle |Oluşturulan bir [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) dizininde. |
| Kümesi temsilci girişi |Güncelleştirilmiş bir [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) dizininde. |
| Temsilci girdiyi kaldırın |Silinmiş bir [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) dizininde. |
| **Rol olayları** | |
| Rol için rol üye ekleme |Bir kullanıcı bir dizin rolüne eklenir. |
| Rol üyesi rolünden Kaldır |Bir kullanıcı dizini rolden kaldırıldı. |
| AddRoleDefinition |Eklenen rol tanımı. |
| UpdateRoleDefinition |Rol tanımı güncelleştirildi. Hangi rolü ayarlar güncelleştirildi görmek için bkz [rol tanımı özellikleri denetlenen](#update-role-definition-attributes) bölümünde |
| DeleteRoleDefinition |Rol tanımı silindi. |
| AddRoleAssignmentToRoleDefinition |Rol tanımı için eklenen rol ataması. |
| RemoveRoleAssignmentFromRoleDefinition |Rol tanımı gelen kaldırılan rol atamasını. |
| AddRoleFromTemplate |Eklenen rolü şablondan. |
| UpdateRole |Güncelleştirilmiş bir roldür. |
| AddRoleScopeMemberToRole |Role eklenen kapsamlı üye. |
| RemoveRoleScopedMemberFromRole |Kapsamlı üye rolünden kaldırıldı. |
| **Aygıt olaylarını (tüm yeni olaylar)** | |
| AddDevice |Eklenen bir cihazı. |
| UpdateDevice |Güncelleştirilmiş cihaz. Hangi cihaz özellikleri güncelleştirildi görmek için bkz [cihaz özellikleri Audited](#update-device-attributes) bölümünde |
| DeleteDevice |Silinen cihaz. |
| AddDeviceConfiguration |Eklenen bir cihazı yapılandırma. |
| UpdateDeviceConfiguration |Güncelleştirilmiş cihaz yapılandırması. Hangi aygıt yapılandırma özelliklerini güncelleştirildi görmek için bkz [aygıt yapılandırma özelliklerini Audited](#update-device-configuration-attributes) bölümünde |
| DeleteDeviceConfiguration |Silinen cihaz yapılandırması. |
| AddRegisteredOwner |Aygıt için eklenen kayıtlı sahip. |
| AddRegisteredUsers |Kayıtlı kullanıcıların cihaza eklenir. |
| RemoveRegisteredOwner |Kayıtlı sahip cihazınızdan kaldırın. |
| RemoveRegisteredUsers |Kayıtlı kullanıcıların CİHAZDAN kaldırın. |
| RemoveDeviceCredentials |Cihaz kimlik bilgilerini kaldırın. |
| **B2B olayları** | |
| Toplu davetiye karşıya yüklendi. |Yönetici iş ortağı kullanıcılara gönderilecek davetleri içeren bir dosya yükledi. |
| İşlenen davetiye toplu. |İş ortağı kullanıcılara davet içeren bir dosyayı işledi. |
| Dış kullanıcı davet edin. |Bir dış kullanıcı dizinine davet. |
| Dış kullanıcı davet kullanın. |Bir dış kullanıcı kendi davet dizinine kullanılan. |
| Dış kullanıcı grubuna ekleyin. |Bir dış kullanıcı Directory'deki bir gruba üyelik atanmıştır. |
| Dış kullanıcı uygulamaya atayın. |Bir dış kullanıcının uygulamaya doğrudan erişim atanmıştır. |
| Virüslü Kiracı oluşturma. |Yeni bir kiracı tarafından davet kullanım Azure AD içinde oluşturuldu. |
| Virüslü kullanıcı oluşturma. |Bir kullanıcı mevcut bir kiracı tarafından davet kullanım Azure AD içinde oluşturuldu. |
| **İdari birim (tüm yeni olaylar)** | |
| AddAdministrativeUnit |Yönetim birimi ekleyin. |
| UpdateAdministrativeUnit |Yönetim birimi güncelleştirin. Hangi yönetim birimi özellikleri güncelleştirildi görmek için bkz [yönetimsel birim denetlenen özellikleri](#update-administrative-unit-attributes) bölümünde |
| DeleteAdministrativeUnit |Yönetim birimi silin. |
| AddMemberToAdministrativeUnit |Üye yönetim birimine ekleyin. |
| RemoveMemberFromAdministrativeUnit |Üye yönetim biriminden kaldırın. |
| **Dizin olayları** | |
| İş ortağı şirkete ekleme |Bir iş ortağı dizine eklendi. |
| İş ortağı şirketten Kaldır |Bir iş ortağı dizinden kaldırıldı. |
| DemotePartner |İş ortağı düşürür. |
| Şirket için etki alanı ekleme |Bir etki alanı dizine eklendi. |
| Şirkete ait etki alanını Kaldır |Bir etki alanı dizinden kaldırıldı. |
| etki alanı güncelleştirme |Bir etki alanı dizini güncelleştirildi. Hangi etki alanı özellikleri güncelleştirildi görmek için bkz [etki alanı denetlenen özellikleri](#update-domain-attributes) bölümünde |
| Etki alanı kimlik doğrulaması |Şirket için varsayılan etki alanı ayarı değiştirildi. |
| Şirket iletişim bilgilerini ayarlama |Şirket düzeyinde kişi tercihlerinizi ayarlayın. Bu, Microsoft Online Services hakkında pazarlama yanı sıra teknik bildirimler için e-posta adresleri içerir. |
| Etki alanında Federasyon ayarlarını belirleme |Bir etki alanı için Federasyon ayarları güncelleştirildi. |
| Etki alanını doğrulayın |Dizin üzerinde bir etki alanı doğrulandı. |
| E-posta doğrulanmış etki alanını doğrulayın |E-posta doğrulama kullanarak dizin üzerindeki etki alanı doğrulandı. |
| Şirket üzerinde DirSyncEnabled bayrağını ayarlayın |Azure AD eşitleme için bir dizin sağlar özelliğini ayarlayın. |
| Parola İlkesi Ayarlama |Kullanıcı parola uzunluğu ve karakter kısıtlamalarını ayarlayın. |
| Şirket Bilgilerini Ayarlama |Şirket düzeyi bilgileri güncelleştirildi. Bkz: [Get-MsolCompanyInformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) daha fazla bilgi için PowerShell cmdlet. |
| SetCompanyAllowedDataLocation |Kümesi şirket veri konumu izin verilir. |
| SetCompanyDirSyncEnabled |DirSyncEnabled bayrağını ayarlayın. |
| SetCompanyDirSyncFeature |DirSync özelliğini ayarlayın. |
| SetCompanyInformation |Kümesi şirket bilgileri. |
| SetCompanyMultiNationalEnabled |Şirket çokuluslu özelliği etkin olarak ayarlayın. |
| SetDirectoryFeatureOnTenant |Kiracı'dizin özelliğini ayarlayın. |
| SetTenantLicenseProperties |Kiracı lisans özellikleri ayarlayın. |
| CreateCompanySettings |Şirket ayarları oluştur |
| UpdateCompanySettings |Şirket ayarlarını güncelleştirin. Hangi şirket özellikleri güncelleştirildi görmek için bkz [şirket denetlenen özellikleri](#update-company-attributes) bölümünde |
| DeleteCompanySettings |Şirket ayarları Sil |
| SetAccidentalDeletionThreshold |Yanlışlıkla silme eşiği ayarlayın. |
| SetRightsManagementProperties |Rights management özellikleri ayarlayın. |
| PurgeRightsManagementProperties |Hak Yönetimi özellikleri Temizle. |
| UpdateExternalSecrets |Dış gizli güncelleştir |
| **İlke olayları (tüm yeni olaylar)** | |
| AddPolicy |İlke ekleyin. |
| UpdatePolicy |İlke güncelleştirin. |
| İlkeyi Sil |İlkeyi silin. |
| AddDefaultPolicyApplication |İlke uygulamaya ekleyin. |
| AddDefaultPolicyServicePrincipal |Hizmet sorumlusu ilkesi ekleyin. |
| RemoveDefaultPolicyApplication |İlke uygulamadan Kaldır. |
| RemoveDefaultPolicyServicePrincipal |İlke hizmet sorumlusu kaldırın. |
| RemovePolicyCredentials |İlke kimlik bilgilerini kaldırın. |

## <a name="audit-report-retention"></a>Rapor bekletme denetleme

En son bekletme hakkında bilgi için [Azure Active Directory rapor bekletme ilkeleri](active-directory-reporting-retention.md).


Raporlama API'si daha uzun bekletme dönemleri bunların denetim olaylarını depolanırken ilgilenen müşteriler için düzenli olarak denetim olayları ayrı veri deposuna çekmek için kullanılır. Bkz: [raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) Ayrıntılar için.

## <a name="properties-included-with-each-audit-event"></a>Her denetim olayı ile dahil özellikleri
| Özellik | Açıklama |
| --- | --- |
| Tarih ve saat |Denetim olayı oluştu saat ve tarihi |
| Aktör |Kullanıcı veya gerçekleştirilen eylem hizmet sorumlusu |
| Eylem |Gerçekleştirilen eylem |
| Hedef |Kullanıcı veya eylem gerçekleştirilip gerçekleştirilmediğine hizmet sorumlusu |

## <a name="update-user-attributes"></a>"Kullanıcı güncelleştir" öznitelikleri
"Güncelleştirme kullanıcı" denetim olayı hangi kullanıcı özniteliklerini güncelleştirildi hakkında ek bilgi içerir. Her öznitelik için önceki değeri ve yeni bir değer eklenmiştir.

| Öznitelik | Açıklama |
| --- | --- |
| accountEnabled |Kullanıcı oturum açabilir. |
| AssignedLicense |Kullanıcıya atanan tüm lisanslar. |
| AssignedPlan |Kullanıcıya atanan lisansları kaynaklanan hizmet planları. |
| LicenseAssignmentDetail |Kullanıcıya atanan lisansları ayrıntıları. Örneğin, Grup tabanlı lisans dahil, bu bir lisans grubu içerir. |
| Cep telefonu |Kullanıcının cep telefonu. |
| OtherMail |Kullanıcının alternatif e-posta adresi. |
| OtherMobile |Kullanıcının diğer cep telefonu. |
| StrongAuthenticationMethod |Sesli arama, SMS ya da doğrulama kodu bir mobil uygulama gibi çok faktörlü kimlik doğrulaması için kullanıcı tarafından yapılandırılan doğrulama yöntemlerin listesi. |
| StrongAuthenticationRequirement |Çok faktörlü kimlik doğrulamasını zorunlu kılındığında, etkin veya bu kullanıcı için devre dışı. |
| StrongAuthenticationUserDetails |Kullanıcının telefon numarasını, alternatif telefon numarası ve e-posta adresi çok faktörlü kimlik doğrulaması ve parola sıfırlama doğrulama için kullanılır. |
| StrongAuthenticationPhoneAppDetail |Ayrıntı forof phone uygulamalarını 2FA oturum açma gerçekleştirmek için kayıtlı |
| telephoneNumber |Kullanıcının telefon numarası. |
| AlternativeSecurityId |Nesne için bir alternatif güvenlik kimliği. |
| CreationType |Kullanıcı (veya davet virüslü) oluşturma yöntemi. |
| InviteTicket |Kullanıcı Davet biletlerini listesi. |
| InviteReplyUrl |Daveti kabul yanıtlamak için URL'lerin listesi. |
| InviteResources |Kullanıcı Davet kaynaklar listesi. |
| LastDirSyncTime |Nesne yetkili eşitleme nedeniyle güncelleştirilen son zamanı (müşteri, şirket içi) dizini. |
| MSExchRemoteRecipientType |MSO alıcı türlerine eşlenir. Alıcı türleri için [MSO alıcı türleri] https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx bakın |
| PreferredDataLocation |Kullanıcının, grubun, kişinin, ortak klasör için tercih edilen konum veya aygıtın verileri. |
| ProxyAddresses |Exchange Server alıcı nesneyi bir yabancı posta sisteminde tanınır adresi. |
| StsRefreshTokensValidFrom |İzleme belirteci iptal bilgilerini Yenile - Bu saat olarak kabul edilir önce verilen herhangi bir STS yenileme belirteçleri süresi doldu. |
| userPrincipalName |Bir kullanıcı için bir Internet stili oturum açma adı UPN. |
| UserState |Kullanıcı PendingApproval/PendingAcceptance/kabul/PendingVerification durumu. |
| UserStateChangedOn |Son değişiklik UserState için zaman damgası. Yaşam döngüsü iş akışları tetiklemek için kullanılır. |
| UserType |Kullanıcı türü. Üye (0), Konuk (1) Viral(2). |

## <a name="update-group-attributes"></a>"Güncelleştirme grubu" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| Sınıflandırma |Bir birleşik grubu (HBI, MBI, vb.) için sınıflandırması. |
| Açıklama |Nesneyle ilgili açıklayıcı tümcecikleri okunabilir. |
| Görünen adı |Bir nesne için görünen ad |
| dirSyncEnabled |Eşitleme bir yetkili olup olmadığını belirtir (müşteri, şirket içi) dizini. |
| GroupLicenseAssignment |Bir grubun lisans atama |
| groupType |Birleştirilmiş grup, (0) türü |
| IsMembershipRuleLocked |MembershipRule özelliği Self Servis Grup Yönetimi hizmeti tarafından ayarlanır ve kullanıcılar tarafından değiştirilemez gösterir. Yalnızca Burada GroupType GroupType.DynamicMembership içeren grupları uygulanabilir |
| IsPublic |Grup ortak/özel olup olmadığını belirtmek için bayraklayın. |
| LastDirSyncTime |Nesne yetkili eşitleme sonucu olarak güncelleştirilen son zamanı (şirket içi, müşteri) dizini. |
| Posta |Birincil e-posta adresi |
| MailEnabled |Bu Grup e-posta özelliğine sahip olup olmadığını gösterir. |
| mailNickname |Bir adres defteri nesnesi için ad, genellikle e-posta adını önceki kısmı "@" simgesi. |
| MembershipRule |Self Servis Grup Yönetimi hizmeti tarafından hangi üyelerinin bu gruba ait belirlemek için kullanılan ölçüt ifade eden bir dize. Ayrıca IsMembershipRuleLocked bakın. Yalnızca Burada GroupType GroupType.DynamicMembership içeren gruplar için geçerli. |
| MembershipRuleProcessingState |Bu grup için işleme üyelik durumunu tanımlama Self Servis Grup Yönetimi hizmeti tarafından tanımlanan bir enum değeri. Yalnızca Burada GroupType GroupType.DynamicMembership içeren gruplar için geçerli. |
| ProxyAddresses |Exchange Server alıcı nesneyi bir yabancı posta sisteminde tanınır adresi. |
| RenewedDateTime |Zaman damgası kaydını bir grup en son ne zaman yenilendi. |
| securityEnabled |Grup üyeliği yetkilendirme kararlarını etkileyebilir olup olmadığını gösterir. |
| WellKnownObject |Önceden tanımlanmış kümesi biri olarak belirleme bir dizin nesnesi etiketler. |

## <a name="update-device-attributes"></a>"Cihaz güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| accountEnabled |Bir güvenlik sorumlusu doğrulanabilir olup olmadığını gösterir. |
| CloudAccountEnabled |Bir güvenlik sorumlusu doğrulanabilir olup olmadığını gösterir. Cihaz şirket içinde yönetilir, Intune tarafından yazılır. |
| CloudDeviceOSType |Aygıt türü işletim sisteminde Windows RT, iOS örneğin temel. Bir bulut hizmeti (örneğin, Intune) olarak ayarlandığında, bu öznitelik için DeviceOSType dizindeki yetkili olur. |
| CloudDeviceOSVersion |İşletim sistemi sürümü. Bir bulut hizmeti (örneğin, Intune) olarak ayarlandığında, bu öznitelik için DeviceOSVersion dizindeki yetkili olur. |
| CloudDisplayName |DisplayName LDAP özniteliğinin değeri. Bir bulut hizmeti (örneğin, Intune) olarak ayarlandığında, bu öznitelik displayName dizininde yetkili olur. |
| CloudCreated |Nesne bulut Hizmetleri tarafından oluşturulup oluşturulmadığını belirtir. |
| CompliantUntil |Ne zamana kadar cihaz uyumlu kabul edilir. |
| DeviceMetadata |Cihaz için özel meta verileri |
| DeviceObjectVersion |Bu öznitelik, cihazın şema sürümü tanımlamak için kullanılır. |
| deviceOSType |Aygıt türü işletim sisteminde Windows RT, iOS örneğin temel. Kayıt hizmeti tarafından yazılmış ve MDM tarafından güncelleştirilecek yönelik yönetim hizmeti veya STS yönetim hizmeti açık. |
| DeviceOSVersion |İşletim sistemi sürümü. Kayıt hizmeti tarafından yazılmış ve MDM tarafından güncelleştirilecek yönelik yönetim hizmeti veya STS yönetim hizmeti açık. |
| DevicePhysicalIds |Fiziksel cihaz tanımlayıcılarını depolamak için amaçlanan birden çok değerli özniteliği. Bu BIOS kimlikleri, TPM parmak izleri, donanım içerebilir belirli kimlikleri, vs. |
| dirSyncEnabled |Eşitleme bir yetkili (müşterinin şirket içi) oluşup oluşmadığını gösterir dizin. |
| Görünen adı |Bir nesne için görünen ad |
| IsCompliant |Bu öznitelik, bir cihazın mobil cihaz Yönetim durumu yönetmek için kullanılır. |
| Ismanaged |Bu öznitelik cihaz bulut MDM tarafından yönetilen belirtmek için kullanılır |
| LastDirSyncTime |Nesne yetkili eşitleme nedeniyle güncelleştirilen son zamanı (şirket içi, müşteri) dizini. |

## <a name="update-device-configuration-attributes"></a>"Aygıt yapılandırması güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| MaximumRegistrationInactivityPeriod |Bir cihazın daha önce devre dışı kalabileceği gün sayısı için temizleme olarak kabul edilir. |
| RegistrationQuota |Tek bir kullanıcı için izin verilen cihaz kayıt sayısını sınırlamak için kullanılan ilkesi. |

## <a name="update-service-principal-configuration-attributes"></a>"Hizmet asıl yapılandırmasını güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| accountEnabled |Bir güvenlik sorumlusu doğrulanabilir olup olmadığını gösterir. |
| Appprincipalıd |Bir güvenlik sorumlusu için dış, uygulama tanımlı kimlik. |
| Görünen adı |Bir nesne için görünen ad |
| ServicePrincipalName |"Ad/burada adı bir uygulama sınıf değeri belirtir ve yetkilisi içeren en az yetkilisi" içeren bir hizmet asıl adı, ana bilgisayar adı [: bağlantı noktası] ya da "name" için hizmet sorumlusu tanımlayıcıyı belirtir. |

## <a name="update-app-attributes"></a>"Uygulama güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| AppAddress |Bir hizmet sorumlusu atanmış olan (URL'leri yönlendirmek) adresleri kümesi. |
| AppID |Uygulamasının uygulama kimliği |
| AppIdentifierUri |Uygulamayı tanımlar uygulaması URI.  Genellikle, uygulama erişim URL'si olur. |
| AppLogoUrl |Bir CDN depolanan uygulama logo görüntüsü URL'si. |
| AvailableToOtherTenants |Uygulama çok kiracılı uygulama geçerlidir (yani diğer kiracılar tarafından kullanılabilir). |
| Görünen adı |Bir uygulama adı için görünen ad |
| Yetkilendirme |Uygulama yetkilendirmeler listesi. |
| ExternalUserAccountDelegationsAllowed |Kaynak uygulama güvenilen bir ve dış kullanıcı hesapları için temsilci girişler oluşturabilirsiniz gösteren bayrak. |
| GroupMembershipClaims |Grup üyeliğini talep ilkesi. |
| PublicClient |İstemci gizli olamaz tutarsanız true (örn. gizli olmayan istemci OAuth2.0 içinde) |
| RecordConsentConditions |Tür sözleşme koşulları tarafından tanımlanan onay koşulu: Hiçbiri (0), SilentConsentForPartnerManagedApp(1). Bu değer grafik API'si şemada sunulur ve yalnızca kümesi/Kiracı Yöneticisi tarafından değiştirilebilir. |
| RequiredResourceAccess |RequiredResourceAccess özelliğinin değeri XML içeriği. |
| WebApp |TRUE ise, bu uygulama bir web uygulaması olduğunu gösterir. |
| WwwHomepage |Birincil Web sayfası. |

## <a name="update-role-attributes"></a>"Rol güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| AppAddress |Bir hizmet sorumlusu atanmış olan (URL'leri yönlendirmek) adresleri kümesi. |
| BelongsToFirstLoginObjectSet |TRUE ise, bu nesnenin ilk yeni bir kiracı Yöneticisi olarak oturum açma etkinleştirmek için gereken nesneler kümesine ait olduğunu gösterir. |
| Yerleşik |Nesne ömrü sistem tarafından ait olup olmadığını gösterir. |
| Açıklama |Nesneyle ilgili açıklayıcı tümcecikleri okunabilir. |
| Görünen adı |Bir nesne için görünen ad |
| mailNickname |Bir adres defteri nesnesi için ad, genellikle e-posta adını önceki kısmı "@" simgesi. |
| RoleDisabled |Rol erişim denetimlerini amaçları doğrultusunda yok sayılıp sayılmayacağını belirtir. |
| RoleTemplateId |Rolü şablonu kimliği. |
| ServiceInfo |MOAC ve/veya diğer hizmet örnekleri (aynı veya farklı hizmet türleri) tarafından tüketilen hizmete özgü sağlama bilgileri. |
| TaskSetScopeReference |Bir TaskSet ve bir rol veya rol şablonu ile ilişkilendirilen kapsamlarını kümesini tanımlar. |
| ValidationError |Özellikler veya çözümlemek için bir nesne yönetici eylemi bağlantısından ilgili geçici olmayan, hizmete özgü bir hatayı açıklayan bir Federasyon Hizmeti tarafından yayımlanan bilgi. |
| WellKnownObject |Önceden tanımlanmış kümesi biri olarak belirleme bir dizin nesnesi etiketler. |

## <a name="update-role-definition-attributes"></a>"Rol tanımı güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| AssignableScopes |Bu RoleDefinition bir güvenlik sorumlusu atarken başvurulabilir yetkilendirme kapsamları koleksiyonu. |
| Görünen adı |Bir nesne için görünen ad |
| GrantedPermissions |Bu RoleDefinition tarafından verilen izinler. |

## <a name="update-administrative-unit-attributes"></a>"Yönetim birimi güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| Açıklama |Bu özellik, bir yönetim birimi açıklaması değiştirdiğinizde güncelleştirilir. |
| Görünen adı |Bir yönetim biriminin adını değiştirdiğinizde, bu özellik güncelleştirilir. |

## <a name="update-company-attributes"></a>"Güncelleştirme şirket" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| AllowedDataLocation |Şirket kullanıcıların hangi sağlanacak izin verilen bir konum. |
| AuthorizedServiceInstance |Bir planı dağıtılmış olabilecek hizmet örneği adları. |
| dirSyncEnabled |Eşitleme bir yetkili (müşterinin şirket içi) oluşup oluşmadığını gösterir dizin. |
| DirSyncStatus |Bu Kiracı bağlamda adres defteri nesnelerin eşitleme bir yetkili (müşterinin şirket içi) oluşup oluşmadığını gösterir dizin; Şirket nesneleri DirSyncEnabled özellikte genişlemesi. |
| DirSyncFeatures |Etkin ve devre dışı dirsync özellikler kümesi Kiracı izlemek için bit bayrağı. |
| DirectoryFeatures |Etkin/devre dışı directory özellikleri. |
| DirSyncConfiguration |Tüm DirSync yapılandırması geçerli Kiracı belirli içeriyor. |
| Görünen adı |Bir nesne için görünen ad |
| IsMnc |Şirket için şirketi özelliği etkinleştirilmişse "true" olur için bir Boole bayrağı ayarlayın. |
| ObjectSettings |Nesne kapsam için geçerli ayarları koleksiyonu. |
| PartnerCommerceUrl |İş ortağının ticaret sitesi URL. |
| PartnerHelpUrl |İş ortağının Yardım site URL'si. |
| PartnerSupportEmail |İş ortağının Destek e-posta URL. |
| PartnerSupportTelephone |İş ortağının destek telefon URL. |
| PartnerSupportUrl |İş ortağının Destek sitesi URL. |
| StrongAuthenticationDetails |StrongAuthentication için ilgili ayrıntıları. |
| StrongAuthenticationPolicy |Şirket için güçlü kimlik doğrulama ilkesi. |
| TechnicalNotificationMail |Bir şirket için ilgili teknik sorunları bildirmek için e-posta adresi. |
| telephoneNumber |ITU öneri E.123 ile uyumlu telefon numaraları. |
| TenantType |Bir kiracı türü. Bu değer belirtilmezse, Kiracı bir şirkettir. Aksi takdirde, olası değerler şunlardır: MicrosoftSupport (0), SyndicatePartner (1), (2) BreadthPartner BreadthPartnerDelegatedAdmin (3) ResellerPartnerDelegatedAdmin (4) ValueAddedResellerPartnerDelegatedAdmin (5). |
| VerifiedDomain |DNS etki alanı adları şirket için bağlı bir dizi. |

## <a name="update-domain-attributes"></a>"Etki alanını güncelleştirmek" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| Özellikler |Varsa etki alanının özelliklerini açıklayan bayrakları bit. |
| Varsayılan |Etki alanı varsayılan değer olup olmadığını gösterir; Yönetici yeni bir kullanıcı MOAC oluşturduğunda, örneğin, varsayılan UserPrincipalName soneki. |
| İlk |Etki alanına ilk etki alanı şirket olup olmadığını OCP tarafından ayrılmış olarak gösterir. İlk etki alanı bir Microsoft Online etki alanının benzersiz bir alt etki alanıdır; e.g.contoso3.microsoftonline.com. |
| LiveType |Türü karşılık gelen Windows Live ad alanının varsa. |
| Ad |Uç nokta için tanımlayıcı. |
| PasswordNotificationWindowDays |Kullanıcının parola süresi dolmadan önce geçmesi gereken gün sayısını bildirilir. |
| PasswordValidityPeriodDays |Bir parolanın değiştirilmesi gerekmeden önce geçmesi için iyi olduğu gün sayısı. |

Denetim, birçok uyumluluk düzenlemeleri için gereken bir denetim kayıtlarıdır. Kendi uyumluluk düzenlemeleri sağlamak için Azure Active Directory denetim raporu kullanarak müşteriler için müşteri bu Yardım konusu bir kopyasını rapor ayrıntıları açıklamaya yardımcı olması için Müşteri'nin dışarı aktarılan denetim rapor kopyasıyla gönderme önerilir. Denetçi Azure şu anda karşılayan uyumluluk düzenlemeleri anlamak istiyorsanız, denetçi doğrudan [uyumluluk sayfası](https://azure.microsoft.com/support/trust-center/compliance/) Microsoft Azure Trust Center.

