---
title: "aaaAzure Active Directory Denetim Raporu olayları | Microsoft Docs"
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
ms.openlocfilehash: 4a84cce2be56bde006164abf10ad1e72ca6e99bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Azure Active Directory denetim raporu olayları
*Bu belge hello parçası olan [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).*

Hello Azure Active Directory denetim raporu, müşterilerin kendi Azure Active Directory'de oluştu ayrıcalıklı Eylemler tanımlamak yardımcı olur. Ayrıcalıklı Eylemler dahil ayrıcalık değişiklikler (örneğin, rolü oluşturma veya parola sıfırlama) ilkesi yapılandırmaları (örneğin, parola ilkelerinin) veya değişiklikleri toodirectory yapılandırması (örneğin, değişiklikleri toodomain Federasyon ayarları) değiştirme. Merhaba raporları hello denetim kaydı hello olay adı, hello eylemin hello değişiklik ve hello tarih ve saat (UTC içinde) etkilenen hello hedef kaynak gerçekleştiren hello aktör sağlar. Müşterilerdir mümkün tooretrieve hello hello aracılığıyla kendi Azure Active Directory için denetim olayları listesini [Azure Portal](https://portal.azure.com/)açıklandığı gibi [denetim günlüklerini görüntülemek](active-directory-reporting-azure-portal.md).

## <a name="list-of-audit-report-events"></a>Denetim Raporu olayları listesi
<!--- audit event descriptions should be in hello past tense --->

| Olaylar | Olay açıklaması |
| --- | --- |
| **Kullanıcı olayları** | |
| Kullanıcı Ekleme |Bir kullanıcı toohello dizini eklendi. |
| Kullanıcıyı Silme |Bir kullanıcı hello dizinden silinir. |
| Lisans özelliklerini ayarlama |Merhaba dizininde bir kullanıcı için Hello lisans özellikleri ayarlayın. |
| Kullanıcı parolasını sıfırlama |Merhaba hello dizininde bir kullanıcı parolasını sıfırlayın. |
| Kullanıcı parolasını değiştirme |Merhaba dizininde bir kullanıcı Hello parolası değiştirildi. |
| Değişiklik kullanıcı lisansı |Merhaba lisansı tooa kullanıcı hello dizinde atanmış değiştirildi. hangi lisansları güncelleştirildi, arama sırasında hello toosee [güncelleştirme kullanıcı](#update-user-attributes) aşağıdaki özellikleri |
| Kullanıcıyı güncelleştirir |Merhaba dizininde bir kullanıcı güncelleştirildi. [Aşağıya bakın](#update-user-attributes) güncelleştirilebilir öznitelikler için. |
| Kullanıcı parolasını değiştirme kümesi zorla |Bir kullanıcı toochange zorlar hello özelliğini oturum açma parolasını ayarlayın. |
| Kullanıcı kimlik bilgilerini güncelleştir |Kullanıcı değişen hello parolası |
| **Grup olayları** | |
| Grup Ekle |Bir grup hello dizininde oluşturuldu. |
| Güncelleştirme grubu |Merhaba Directory'deki bir gruba güncelleştirildi. hangi Grup Özellikleri güncelleştirildi, toosee başvuran çok[Grup Özellikleri denetlenen](#update-group-attributes) hello bölümünde aşağıdaki |
| Grup silme |Bir grup hello dizinden silinir. |
| CreateGroupSettings |Oluşturulan Grup ayarları |
| UpdateGroupSettings |Grup ayarları güncelleştirildi. hangi Grup ayarları güncelleştirildi, toosee başvuran çok[Grup Özellikleri denetlenen](#update-group-attributes) hello bölümünde aşağıdaki |
| DeleteGroupSettings |Silinen grup ayarları |
| SetGroupLicense |Grup lisans ayarlayın. |
| SetGroupManagedBy |Kullanıcı tarafından yönetilen Grup toobe ayarlayın |
| AddGroupMember |Eklenen üye toogroup |
| RemoveGroupMember |Grubundan üye kaldırma |
| AddGroupOwner |Eklenen sahibi toogroup |
| RemoveGroupOwner |Gruptan kaldırılan sahibi |
| **Uygulama olayları** | |
| Hizmet sorumlusu ekleme |Bir hizmet asıl toohello dizini eklendi. |
| Hizmet sorumlusu Kaldır |Bir hizmet sorumlusu hello dizininden kaldırıldı. |
| Hizmet asıl kimlik bilgileri ekleme |Ek kimlik bilgileri tooa hizmet sorumlusu. |
| Hizmet asıl kimlik bilgilerini kaldırma |Bir hizmet sorumlusu kaldırılan kimlik bilgileri. |
| Temsilci Girişi Ekle |Oluşturulan bir [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) hello dizininde. |
| Kümesi temsilci girişi |Güncelleştirilmiş bir [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) hello dizininde. |
| Temsilci girdiyi kaldırın |Silinmiş bir [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) hello dizininde. |
| **Rol olayları** | |
| Rolü üyesi tooRole Ekle |Bir kullanıcı tooa dizin rolü eklendi. |
| Rol üyesi rolünden Kaldır |Bir kullanıcı dizini rolden kaldırıldı. |
| AddRoleDefinition |Eklenen rol tanımı. |
| UpdateRoleDefinition |Rol tanımı güncelleştirildi. hangi rolü ayarlarını güncelleştirildi, toosee başvuran çok[rol tanımı özellikleri denetlenen](#update-role-definition-attributes) hello bölümünde aşağıdaki |
| DeleteRoleDefinition |Rol tanımı silindi. |
| AddRoleAssignmentToRoleDefinition |Rol atama toorole tanımına eklenir. |
| RemoveRoleAssignmentFromRoleDefinition |Rol tanımı gelen kaldırılan rol atamasını. |
| AddRoleFromTemplate |Eklenen rolü şablondan. |
| UpdateRole |Güncelleştirilmiş bir roldür. |
| AddRoleScopeMemberToRole |Kapsamlı üye toorole eklendi. |
| RemoveRoleScopedMemberFromRole |Kapsamlı üye rolünden kaldırıldı. |
| **Aygıt olaylarını (tüm yeni olaylar)** | |
| AddDevice |Eklenen bir cihazı. |
| UpdateDevice |Güncelleştirilmiş cihaz. hangi cihaz özellikleri güncelleştirildi, toosee başvuran çok[cihaz özellikleri Audited](#update-device-attributes) hello bölümünde aşağıdaki |
| DeleteDevice |Silinen cihaz. |
| AddDeviceConfiguration |Eklenen bir cihazı yapılandırma. |
| UpdateDeviceConfiguration |Güncelleştirilmiş cihaz yapılandırması. hangi aygıt yapılandırma özelliklerini güncelleştirildi, toosee başvuran çok[aygıt yapılandırma özelliklerini Audited](#update-device-configuration-attributes) hello bölümünde aşağıdaki |
| DeleteDeviceConfiguration |Silinen cihaz yapılandırması. |
| AddRegisteredOwner |Kayıtlı sahip toodevice eklendi. |
| AddRegisteredUsers |Kayıtlı kullanıcıların toodevice eklendi. |
| RemoveRegisteredOwner |Kayıtlı sahip cihazınızdan kaldırın. |
| RemoveRegisteredUsers |Kayıtlı kullanıcıların CİHAZDAN kaldırın. |
| RemoveDeviceCredentials |Cihaz kimlik bilgilerini kaldırın. |
| **B2B olayları** | |
| Toplu davetiye karşıya yüklendi. |Bir yönetici toopartner kullanıcılara gönderilen davetleri toobe içeren bir dosya yükledi. |
| İşlenen davetiye toplu. |Davetiye toopartner kullanıcıları içeren bir dosyayı işledi. |
| Dış kullanıcı davet edin. |Bir dış kullanıcı davet edilen toohello dizin olmuştur. |
| Dış kullanıcı davet kullanın. |Bir dış kullanıcı, daveti toohello dizinlerini kullanılan. |
| Dış kullanıcı toogroup ekleyin. |Bir dış kullanıcının üyelik tooa grubu hello dizininde atanmıştır. |
| Dış kullanıcı tooapplication atayın. |Bir dış kullanıcının doğrudan erişim tooan uygulama atanmıştır. |
| Virüslü Kiracı oluşturma. |Yeni bir kiracı Azure AD'de hello davet kullanım tarafından oluşturuldu. |
| Virüslü kullanıcı oluşturma. |Bir kullanıcı, hello davet kullanım tarafından Azure AD'de mevcut bir kiracı oluşturuldu. |
| **İdari birim (tüm yeni olaylar)** | |
| AddAdministrativeUnit |Yönetim birimi ekleyin. |
| UpdateAdministrativeUnit |Yönetim birimi güncelleştirin. hangi yönetim birimi özellikleri güncelleştirildi, toosee başvuran çok[yönetimsel birim denetlenen özellikleri](#update-administrative-unit-attributes) hello bölümünde aşağıdaki |
| DeleteAdministrativeUnit |Yönetim birimi silin. |
| AddMemberToAdministrativeUnit |Üye tooadministrative Birim ekleyin. |
| RemoveMemberFromAdministrativeUnit |Üye yönetim biriminden kaldırın. |
| **Dizin olayları** | |
| İş ortağı toocompany Ekle |Bir iş ortağı toohello dizin eklendi. |
| İş ortağı şirketten Kaldır |Bir iş ortağı hello dizininden kaldırıldı. |
| DemotePartner |İş ortağı düşürür. |
| Etki alanı toocompany Ekle |Bir etki alanı toohello dizin eklendi. |
| Şirkete ait etki alanını Kaldır |Bir etki alanı hello dizininden kaldırıldı. |
| etki alanı güncelleştirme |Bir etki alanı hello dizini güncelleştirildi. Hangi etki alanı özellikleri güncelleştirildi, toosee başvuran çok[etki alanı denetlenen özellikleri](#update-domain-attributes) hello bölümünde aşağıdaki |
| Etki alanı kimlik doğrulaması |Merhaba şirket için Hello varsayılan etki alanı ayarı değiştirildi. |
| Şirket iletişim bilgilerini ayarlama |Şirket düzeyinde kişi tercihlerinizi ayarlayın. Bu, Microsoft Online Services hakkında pazarlama yanı sıra teknik bildirimler için e-posta adresleri içerir. |
| Etki alanında Federasyon ayarlarını belirleme |Bir etki alanı için Hello Federasyon ayarları güncelleştirildi. |
| Etki alanını doğrulayın |Merhaba dizin etki alanı doğrulandı. |
| E-posta doğrulanmış etki alanını doğrulayın |E-posta doğrulama kullanarak hello dizin etki alanı doğrulandı. |
| Şirket üzerinde DirSyncEnabled bayrağını ayarlayın |Azure AD eşitleme için bir dizin sağlayan hello özelliğini ayarlayın. |
| Parola İlkesi Ayarlama |Kullanıcı parola uzunluğu ve karakter kısıtlamalarını ayarlayın. |
| Şirket Bilgilerini Ayarlama |Güncelleştirilmiş hello şirket düzeyi bilgileri. Merhaba bkz [Get-MsolCompanyInformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) daha fazla bilgi için PowerShell cmdlet. |
| SetCompanyAllowedDataLocation |Kümesi şirket veri konumu izin verilir. |
| SetCompanyDirSyncEnabled |DirSyncEnabled bayrağını ayarlayın. |
| SetCompanyDirSyncFeature |DirSync özelliğini ayarlayın. |
| SetCompanyInformation |Kümesi şirket bilgileri. |
| SetCompanyMultiNationalEnabled |Şirket çokuluslu özelliği etkin olarak ayarlayın. |
| SetDirectoryFeatureOnTenant |Kiracı'dizin özelliğini ayarlayın. |
| SetTenantLicenseProperties |Kiracı lisans özellikleri ayarlayın. |
| CreateCompanySettings |Şirket ayarları oluştur |
| UpdateCompanySettings |Şirket ayarlarını güncelleştirin. hangi şirket özellikleri güncelleştirildi, toosee başvuran çok[şirket denetlenen özellikleri](#update-company-attributes) hello bölümünde aşağıdaki |
| DeleteCompanySettings |Şirket ayarları Sil |
| SetAccidentalDeletionThreshold |Yanlışlıkla silme eşiği ayarlayın. |
| SetRightsManagementProperties |Rights management özellikleri ayarlayın. |
| PurgeRightsManagementProperties |Hak Yönetimi özellikleri Temizle. |
| UpdateExternalSecrets |Dış gizli güncelleştir |
| **İlke olayları (tüm yeni olaylar)** | |
| AddPolicy |İlke ekleyin. |
| UpdatePolicy |İlke güncelleştirin. |
| İlkeyi Sil |İlkeyi silin. |
| AddDefaultPolicyApplication |İlke tooapplication ekleyin. |
| AddDefaultPolicyServicePrincipal |İlke tooservice asıl ekleyin. |
| RemoveDefaultPolicyApplication |İlke uygulamadan Kaldır. |
| RemoveDefaultPolicyServicePrincipal |İlke hizmet sorumlusu kaldırın. |
| RemovePolicyCredentials |İlke kimlik bilgilerini kaldırın. |

## <a name="audit-report-retention"></a>Rapor bekletme denetleme

Merhaba en son bekletme hakkında bilgi için [Azure Active Directory rapor bekletme ilkeleri](active-directory-reporting-retention.md).


Müşteriler için daha uzun bekletme dönemleri bunların denetim olaylarını depolanırken ilgilenen, hello raporlama API'si kullanılan tooregularly çekme denetim olayları ayrı veri deposuna olabilir. Bkz: [hello raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) Ayrıntılar için.

## <a name="properties-included-with-each-audit-event"></a>Her denetim olayı ile dahil özellikleri
| Özellik | Açıklama |
| --- | --- |
| Tarih ve saat |Denetim olayı hello Hello tarih ve saat oluştu |
| Aktör |Merhaba kullanıcı veya hello gerçekleştirdiğini hizmet sorumlusu |
| Eylem |gerçekleştirildi hello eylemi |
| Hedef |Merhaba kullanıcı veya eylemin hello hizmet sorumlusu üzerinde gerçekleştirildi |

## <a name="update-user-attributes"></a>"Kullanıcı güncelleştir" öznitelikleri
Güncelleştirme Hello "kullanıcı" denetim olayı hangi kullanıcı özniteliklerini güncelleştirildi hakkında ek bilgi içerir. Her bir öznitelik için hem de önceki değeri hello ve hello yeni değer yer alır.

| Öznitelik | Açıklama |
| --- | --- |
| accountEnabled |Merhaba kullanıcı oturum açabilir. |
| AssignedLicense |Toohello kullanıcı atanan tüm lisanslar. |
| AssignedPlan |Hizmet planları Hello lisanslarını kaynaklanan toohello kullanıcı atanır. |
| LicenseAssignmentDetail |Lisansları atanmış toohello kullanıcı ayrıntıları. Örneğin, Grup tabanlı lisans dahil, bu verilen lisans hello hello grubu içerir. |
| Cep telefonu |Merhaba kullanıcının cep telefonu. |
| OtherMail |kullanıcının alternatif e-posta adresi hello. |
| OtherMobile |kullanıcının diğer cep telefonu hello. |
| StrongAuthenticationMethod |Sesli arama, SMS ya da doğrulama kodu bir mobil uygulama gibi hello kullanıcı tarafından çok faktörlü kimlik doğrulaması için yapılandırılmış doğrulama yöntemleri listesi. |
| StrongAuthenticationRequirement |Çok faktörlü kimlik doğrulamasını zorunlu kılındığında, etkin veya bu kullanıcı için devre dışı. |
| StrongAuthenticationUserDetails |Merhaba kullanıcının number, alternatif bir telefon numarası ve e-posta adresi çok faktörlü kimlik doğrulaması için kullanılan ve doğrulama parola sıfırlama telefon. |
| StrongAuthenticationPhoneAppDetail |Ayrıntı forof phone uygulamalarını tooperform 2FA oturum açma kayıtlı |
| telephoneNumber |Merhaba kullanıcının telefon numarası. |
| AlternativeSecurityId |Merhaba nesne için bir alternatif güvenlik kimliği. |
| CreationType |Merhaba kullanıcı (veya davet virüslü) oluşturma yöntemi. |
| InviteTicket |Merhaba kullanıcı davet biletlerini listesi. |
| InviteReplyUrl |Daveti kabul bağlı URL'leri tooreply listesi. |
| InviteResources |Kaynakları toowhich hello kullanıcı listesini davet. |
| LastDirSyncTime |Son zamanı hello nesne hello yetkili (müşteri, şirket içi) eşitleme nedeniyle güncelleştirildi dizin. |
| MSExchRemoteRecipientType |TooMSO alıcı türleri eşleştirir. Çok bakın [MSO alıcı türleri] https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx alıcı türleri |
| PreferredDataLocation |Merhaba kullanıcının, grubun, kişinin, ortak klasör için tercih edilen konumu ya da cihazın veri hello. |
| ProxyAddresses |Merhaba adresi bir Exchange Server alıcı nesne bir yabancı posta sisteminde tanınır. |
| StsRefreshTokensValidFrom |İzleme belirteci iptal bilgilerini Yenile - Bu saat olarak kabul edilir önce verilen herhangi bir STS yenileme belirteçleri süresi doldu. |
| userPrincipalName |bir kullanıcı için bir Internet stili oturum açma adı UPN Hello. |
| UserState |Kullanıcı PendingApproval/PendingAcceptance/kabul/PendingVerification durumu. |
| UserStateChangedOn |Son değişiklik tooUserState damgası. Kullanılan tootrigger yaşam döngüsü iş akışları. |
| UserType |Kullanıcı türü. Üye (0), Konuk (1) Viral(2). |

## <a name="update-group-attributes"></a>"Güncelleştirme grubu" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| Sınıflandırma |Merhaba sınıflandırması Unified grubunun (HBI, MBI, vb.). |
| Açıklama |Okunabilir açıklayıcı tümcecikleri hello nesne hakkında. |
| Görünen adı |bir nesne için Hello görünen adı |
| dirSyncEnabled |Eşitleme bir yetkili olup olmadığını belirtir (müşteri, şirket içi) dizini. |
| GroupLicenseAssignment |Bir grubun lisans atama |
| groupType |Birleştirilmiş grup, (0) türü |
| IsMembershipRuleLocked |Bu hello MembershipRule özelliği hello Self Servis Grup Yönetimi hizmeti tarafından ayarlanır ve kullanıcılar tarafından değiştirilemez gösterir. Geçerli yalnızca toogroups burada GroupType GroupType.DynamicMembership içerir |
| IsPublic |Merhaba grubu ortak/özel ise tooindicate bayrak. |
| LastDirSyncTime |Son zamanı hello nesne hello yetkili (şirket içi, müşteri) gelen eşitleme sonucu olarak güncelleştirildi dizin. |
| Posta |Birincil e-posta adresi |
| MailEnabled |Bu Grup e-posta özelliğine sahip olup olmadığını gösterir. |
| mailNickname |Bir adres defteri nesnesi için ad, genellikle e-posta adını hello önceki hello bölümünü "@" simgesi. |
| MembershipRule |Hello Self Servis Grup Yönetimi Hizmeti toodetermine tarafından kullanılan hello ölçütleri ifade eden bir dize olan üyeleri toothis grubuna ait olmalıdır. Ayrıca IsMembershipRuleLocked bakın. Geçerli yalnızca toogroups burada GroupType GroupType.DynamicMembership içerir. |
| MembershipRuleProcessingState |Bu grup için işleme üyelik hello durumunu tanımlama hello Self Servis Grup Yönetimi hizmeti tarafından tanımlanan bir enum değeri. Geçerli yalnızca toogroups burada GroupType GroupType.DynamicMembership içerir. |
| ProxyAddresses |Merhaba adresi bir Exchange Server alıcı nesne bir yabancı posta sisteminde tanınır. |
| RenewedDateTime |Zaman damgası kaydını bir grup en son ne zaman yenilendi. |
| securityEnabled |Merhaba grubu üyeliği yetkilendirme kararlarını etkileyebilir olup olmadığını gösterir. |
| WellKnownObject |Önceden tanımlanmış kümesi biri olarak belirleme bir dizin nesnesi etiketler. |

## <a name="update-device-attributes"></a>"Cihaz güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| accountEnabled |Bir güvenlik sorumlusu doğrulanabilir olup olmadığını gösterir. |
| CloudAccountEnabled |Bir güvenlik sorumlusu doğrulanabilir olup olmadığını gösterir. Merhaba cihaz şirket içinde yönetilir, Intune tarafından yazılır. |
| CloudDeviceOSType |Örneğin Windows RT, iOS işletim sistemi hello üzerinde temel hello aygıt türü. Bir bulut hizmeti (örneğin, Intune) olarak ayarlandığında, bu öznitelik için DeviceOSType hello dizininde yetkili olur. |
| CloudDeviceOSVersion |Merhaba işletim sistemi sürümü. Bir bulut hizmeti (örneğin, Intune) olarak ayarlandığında, bu öznitelik için DeviceOSVersion hello dizininde yetkili olur. |
| CloudDisplayName |Merhaba displayName LDAP özniteliğinin değeri. Bir bulut hizmeti (örneğin, Intune) olarak ayarlandığında, bu öznitelik hello dizininde displayName için yetkili haline gelir. |
| CloudCreated |Merhaba nesne bulut Hizmetleri tarafından oluşturulup oluşturulmadığını belirtir. |
| CompliantUntil |Ne zamana kadar cihaz uyumlu kabul edilir. |
| DeviceMetadata |Merhaba cihaz için özel meta verileri |
| DeviceObjectVersion |Bu öznitelik kullanılan tooidentify hello şema hello aygıt sürümüdür. |
| deviceOSType |Örneğin Windows RT, iOS işletim sistemi hello üzerinde temel hello aygıt türü. Tarafından yazılan hello kayıt hizmeti ve hedeflenen toobe tarafından hello MDM yönetim hizmeti güncelleştirilmiş veya STS yönetim hizmeti açık. |
| DeviceOSVersion |Merhaba işletim sistemi sürümü. Tarafından yazılan hello kayıt hizmeti ve hedeflenen toobe tarafından hello MDM yönetim hizmeti güncelleştirilmiş veya STS yönetim hizmeti açık. |
| DevicePhysicalIds |Birden çok değerli öznitelik hello fiziksel aygıt toostore tanımlayıcıları amaçlanmıştır. Bu BIOS kimlikleri, TPM parmak izleri, donanım içerebilir belirli kimlikleri, vs. |
| dirSyncEnabled |Eşitleme bir yetkili (müşterinin şirket içi) oluşup oluşmadığını gösterir dizin. |
| Görünen adı |bir nesne için Hello görünen adı |
| IsCompliant |Kullanılan toomanage hello mobil cihaz Yönetim durumu hello cihazın özniteliğidir. |
| Ismanaged |Bu öznitelik kullanılan tooindicate hello cihaz bulut MDM tarafından yönetilen |
| LastDirSyncTime |Son zamanı hello nesne hello yetkili (şirket içi, müşteri) gelen eşitleme nedeniyle güncelleştirildi dizin. |

## <a name="update-device-configuration-attributes"></a>"Aygıt yapılandırması güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| MaximumRegistrationInactivityPeriod |kaldırma için kabul edilmeden önce hello en fazla gün sayısı bir aygıtı devre dışı olabilir. |
| RegistrationQuota |İlke olan tek bir kullanıcı için izin verilen cihaz kaydı toolimit hello sayısı kullanılır. |

## <a name="update-service-principal-configuration-attributes"></a>"Hizmet asıl yapılandırmasını güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| accountEnabled |Bir güvenlik sorumlusu doğrulanabilir olup olmadığını gösterir. |
| Appprincipalıd |Bir güvenlik sorumlusu için dış, uygulama tanımlı kimlik. |
| Görünen adı |bir nesne için Hello görünen adı |
| ServicePrincipalName |"Ad/burada adı bir uygulama sınıf değeri belirtir ve yetkilisi içeren en az yetkilisi" içeren bir hizmet asıl adı, ana bilgisayar adı [: bağlantı noktası] ya da "name" Merhaba hizmet sorumlusu için bir tanımlayıcı belirtir. |

## <a name="update-app-attributes"></a>"Uygulama güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| AppAddress |tooa hizmet sorumlusu atanan (URL'leri yönlendirmek) adresleri kümesini Hello. |
| AppID |Uygulama Kimliğini hello uygulama |
| AppIdentifierUri |Merhaba uygulamayı tanımlar uygulaması URI.  Bu genellikle hello uygulama erişim URL'dir. |
| AppLogoUrl |bir CDN depolanan hello uygulama logo görüntüsü Hello URL'si. |
| AvailableToOtherTenants |Doğru hello uygulamasıdır çok kiracılı uygulama (yani diğer kiracılar tarafından kullanılabilir). |
| Görünen adı |bir uygulama adı Hello görünen adı |
| Yetkilendirme |Uygulama yetkilendirmeler listesi. |
| ExternalUserAccountDelegationsAllowed |Kaynak uygulama güvenilen bir ve dış kullanıcı hesapları için temsilci girişler oluşturabilirsiniz gösteren bayrak. |
| GroupMembershipClaims |Merhaba grup üyeliğini talep ilkesi. |
| PublicClient |Merhaba istemci gizli olamaz tutarsanız true (örn. gizli olmayan istemci OAuth2.0 içinde) |
| RecordConsentConditions |Tür onay koşulu hello tarafından tanımlanan sözleşme koşullarını: Hiçbiri (0), SilentConsentForPartnerManagedApp(1). Bu değer hello grafik API'si şemada sunulur ve yalnızca kümesi/Kiracı Yöneticisi tarafından değiştirilebilir. |
| RequiredResourceAccess |Merhaba RequiredResourceAccess özellik değerini XML içeriği. |
| WebApp |TRUE ise, bu uygulama bir web uygulaması olduğunu gösterir. |
| WwwHomepage |Merhaba birincil Web sayfası. |

## <a name="update-role-attributes"></a>"Rol güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| AppAddress |tooa hizmet sorumlusu atanan (URL'leri yönlendirmek) adresleri kümesini Hello. |
| BelongsToFirstLoginObjectSet |TRUE ise, bu nesne nesneleri gerekli tooenable oturum açma hello ilk yöneticisinin yeni bir kiracı toohello kümesi ait olduğunu gösterir. |
| Yerleşik |Nesne ömrü Hello hello sistem tarafından ait olup olmadığını gösterir. |
| Açıklama |Okunabilir açıklayıcı tümcecikleri hello nesne hakkında. |
| Görünen adı |bir nesne için Hello görünen adı |
| mailNickname |Bir adres defteri nesnesi için ad, genellikle e-posta adını hello önceki hello bölümünü "@" simgesi. |
| RoleDisabled |Merhaba rol erişim denetimlerini amaçları doğrultusunda yok sayılıp sayılmayacağını belirtir. |
| RoleTemplateId |Merhaba rolü şablonu kimliği. |
| ServiceInfo |Hizmete özgü MOAC ve/veya diğer hizmet örneği tarafından kullanılan bilgileri sağlama (aynı veya farklı Merhaba, hizmet türleri). |
| TaskSetScopeReference |Bir TaskSet ve bir rol veya rol şablonu ile ilişkilendirilen kapsamlarını kümesini tanımlar. |
| ValidationError |Merhaba özellikleri veya bir nesne yönetici eylemi tooresolve bağlantısından ilgili geçici olmayan, hizmete özgü bir hatayı açıklayan bir Federasyon Hizmeti tarafından yayımlanan bilgi. |
| WellKnownObject |Önceden tanımlanmış kümesi biri olarak belirleme bir dizin nesnesi etiketler. |

## <a name="update-role-definition-attributes"></a>"Rol tanımı güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| AssignableScopes |Bu RoleDefinition tooa güvenlik sorumlusu atarken başvurulabilir yetkilendirme kapsamları koleksiyonu. |
| Görünen adı |bir nesne için Hello görünen adı |
| GrantedPermissions |Bu RoleDefinition tarafından verilen izinler. |

## <a name="update-administrative-unit-attributes"></a>"Yönetim birimi güncelleştir" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| Açıklama |Bu özellik, bir yönetim birimi hello açıklaması değiştirdiğinizde güncelleştirilir. |
| Görünen adı |Bu özellik, bir yönetim birimi hello adını değiştirmek güncelleştirilir. |

## <a name="update-company-attributes"></a>"Güncelleştirme şirket" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| AllowedDataLocation |Hangi hello şirketin kullanıcıların sağlanan toobe izin verilen bir konum. |
| AuthorizedServiceInstance |Hizmet örnekleri toowhich bir planı adlarını dağıtılabilir. |
| dirSyncEnabled |Eşitleme bir yetkili (müşterinin şirket içi) oluşup oluşmadığını gösterir dizin. |
| DirSyncStatus |Bu Kiracı bağlamda adres defteri nesnelerin eşitleme bir yetkili (müşterinin şirket içi) oluşup oluşmadığını gösterir dizin; Merhaba DirSyncEnabled özelliği şirket nesneler üzerinde Genişletilmiş. |
| DirSyncFeatures |Merhaba Kiracı için etkin ve devre dışı dirsync özellik kümesinden bit bayrağı tookeep izleme. |
| DirectoryFeatures |Etkin/devre dışı directory özellikleri. |
| DirSyncConfiguration |Tüm DirSync yapılandırması belirli toohello geçerli Kiracı içerir. |
| Görünen adı |bir nesne için Hello görünen adı |
| IsMnc |Bir Boole bayrak kümesi "true" çok olur hello şirket hello şirketi özelliği etkinleştirilir. |
| ObjectSettings |Merhaba nesnesinin ayarları uygulanabilir toohello kapsamı koleksiyonu. |
| PartnerCommerceUrl |URL toohello ortağın ticaret sitesi. |
| PartnerHelpUrl |URL toohello ortağın Yardım sitesi. |
| PartnerSupportEmail |URL toohello ortağın Destek e-posta. |
| PartnerSupportTelephone |URL toohello ortağın destek telefon. |
| PartnerSupportUrl |URL toohello ortağın Destek sitesi. |
| StrongAuthenticationDetails |TooStrongAuthentication ilgili ayrıntıları. |
| StrongAuthenticationPolicy |Merhaba şirket için güçlü kimlik doğrulama ilkesi. |
| TechnicalNotificationMail |Tooa şirket ilgili e-posta adresi toonotify teknik sorunları. |
| telephoneNumber |Merhaba ITU öneri E.123 ile uyumlu telefon numaraları. |
| TenantType |bir kiracı Hello türü. Bu değer belirtilmezse, hello Kiracı bir şirkettir. Aksi takdirde, olası değerler şunlardır: MicrosoftSupport (0), SyndicatePartner (1), (2) BreadthPartner BreadthPartnerDelegatedAdmin (3) ResellerPartnerDelegatedAdmin (4) ValueAddedResellerPartnerDelegatedAdmin (5). |
| VerifiedDomain |DNS etki alanı adları bir dizi tooa şirket bağlı. |

## <a name="update-domain-attributes"></a>"Etki alanını güncelleştirmek" öznitelikleri
| Öznitelik | Açıklama |
| --- | --- |
| Özellikler |Bit hello etki alanının açıklayan hello özellikleri varsa işaretler. |
| Varsayılan |Merhaba etki alanı hello varsayılan değer olup olmadığını gösterir; Yönetici yeni bir kullanıcı MOAC oluşturduğunda, örneğin, hello varsayılan UserPrincipalName soneki. |
| İlk |Merhaba etki alanı hello hello şirket için ilk etki alanı olup olmadığını OCP tarafından ayrılmış olarak gösterir. Merhaba ilk etki alanı bir Microsoft Online etki alanının benzersiz bir alt etki alanıdır; e.g.contoso3.microsoftonline.com. |
| LiveType |Merhaba karşılık gelen Windows Live ad alanı, varsa türü. |
| Ad |Merhaba uç noktası için tanımlayıcı. |
| PasswordNotificationWindowDays |Merhaba hello kullanıcının parola süresi dolmadan önce gün sayısı bildirilir. |
| PasswordValidityPeriodDays |Merhaba değiştirilmesi gerekmeden önce bir parola için iyi olduğu gün sayısı. |

Denetim, birçok uyumluluk düzenlemeleri için gereken bir denetim kayıtlarıdır. Kendi uyumluluk düzenlemeleri Hello Azure Active Directory denetim raporu toomeet kullanan müşteriler için o hello müşteri gönderme kopyayla hello Müşteri'nin hello kopyasını bu Yardım konusu toohelp hello rapor açıklayan denetim raporu dışarı önerilir. Ayrıntıları. Merhaba denetçi Azure şu anda karşılayan toounderstand hello uyumluluk düzenlemeleri kullanmak isterseniz, hello denetçi toohello doğrudan [uyumluluk sayfası](https://azure.microsoft.com/support/trust-center/compliance/) hello Microsoft Azure Trust Center.

