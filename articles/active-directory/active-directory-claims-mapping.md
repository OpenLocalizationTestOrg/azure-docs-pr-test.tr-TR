---
title: "Talep eşleme Azure Active Directory'de (genel Önizleme) | Microsoft Docs"
description: "Bu sayfa, Azure Active Directory talep eşleme açıklar."
services: active-directory
author: billmath
manager: femila
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: ff07b9954d5c2ce71ab0ffd0db49fde15f323586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a>Azure Active Directory'de (genel Önizleme) eşleme talepleri

>[!NOTE]
>Bu özellik değiştirir ve hello yerine geçiyor [özelleştirme talep](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) bugün hello Portalı aracılığıyla sunulan. Merhaba portal kullanarak talep özelleştirirseniz ayrıca toohello grafik/PowerShell yöntemi hello bu belgeyi aynı ayrıntılı uygulama, uygulama hello portal hello yapılandırmasında yoksayacak verilen belirteçleri.
Bu belgede ayrıntılı hello yöntemleri aracılığıyla yapılan yapılandırmalar hello Portalı'nda yansıtılmaz.

Bu özellik, Kiracı yöneticileri toocustomize hello talep kendi Kiracı içinde belirli bir uygulamayı belirteçlerinde yayılan tarafından kullanılır. İlkeleri için eşleme talep kullanabilirsiniz:

- Hangi taleplerin belirteçleri dahil edilen seçin.
- Henüz yoksa talep türlerini oluşturun.
- Seçebilir veya belirli Taleplerde yayılan veriler hello kaynağını değiştirme.

>[!NOTE]
>Bu özellik şu anda genel önizlemede değil. Toorevert hazırlanması veya herhangi bir değişiklik kaldırın. Genel Önizleme sırasında herhangi bir Azure Active Directory (Azure AD) abonelik Hello özelliği kullanılabilir. Ancak, Hello özelliği genel kullanıma sunulduğunda hello özelliği bazı yönlerini bir Azure Active Directory premium aboneliği gerektirebilir.

## <a name="claims-mapping-policy-type"></a>İlke türü eşleme talepleri
Azure AD'de bir **İlkesi** nesnesi, tek tek uygulamalar veya bir kuruluştaki tüm uygulamaları zorlanan kurallar kümesini temsil eder. Her ilke türü bir özellikler kümesi ile benzersiz bir yapıya sahip sonra atanmışlarsa tooobjects toowhich uygulanır.

Bir talep ilke eşleme türüdür **İlkesi** hello değiştirir nesne talep yayılan belirli uygulamalar için verilen belirteçlerinde.

## <a name="claim-sets"></a>Talep kümeleri
Belirli nasıl ve ne zaman belirteçleri kullanıldıkları tanımlayan talep kümesi vardır.

### <a name="core-claim-set"></a>Çekirdek talep kümesi
Talep hello çekirdek talepler kümesi İlkesi bağımsız olarak her belirteçte mevcut. Bu talep sınırlı kabul edilir ve değiştirilemez.

### <a name="basic-claim-set"></a>Temel talep kümesi
Merhaba temel talep kümesi belirteçlerinde (toplama toohello çekirdek talep kümesi) için varsayılan olarak gösterilen hello talepleri içerir. Bu talep atlanmış veya ilkeleri eşleme hello talep kullanılarak değiştirilebilir.

### <a name="restricted-claim-set"></a>Kısıtlı talep kümesi
Kısıtlı talep İlkesi kullanılarak değiştirilemez. Merhaba veri kaynağı değiştirilemez ve hiçbir dönüştürme bu talepler oluştururken uygulanır.

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a>Tablo 1: JSON Web Token (JWT) talep kümesi kısıtlanmış.
|Talep türü (ad)|
| ----- |
|_claim_names|
|_claim_sources|
|access_token|
|account_type|
|ACR|
|Aktör|
|actortoken|
|AIO|
|altsecid|
|amr|
|app_chain|
|app_displayname|
|app_res|
|appctx|
|appctxsender|
|AppID|
|appidacr|
|onaylama işlemi|
|at_hash|
|aud|
|auth_data|
|auth_time|
|authorization_code|
|azp|
|azpacr|
|c_hash|
|ca_enf|
|Cc|
|cert_token_use|
|client_id|
|cloud_graph_host_name|
|cloud_instance_name|
|cnf|
|Kod|
|denetimler|
|credential_keys|
|CSR|
|csr_type|
|cihaz kimliği|
|dns_names|
|domain_dns_name|
|domain_netbios_name|
|e_exp|
|E-posta|
|uç noktası|
|enfpolids|
|exp|
|expires_on|
|grant_type|
|Grafik|
|group_sids|
|gruplar|
|hasgroups|
|hash_alg|
|home_oid|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/AuthenticationMethod|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/Expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/Expired|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/emailaddress|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/Name|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/nameidentifier|
|IAT|
|ıdentityprovider|
|IDP|
|in_corp|
|Örneği|
|IpAddr|
|isbrowserhostedapp|
|ISS|
|jwk|
|key_id|
|key_type|
|mam_compliance_url|
|mam_enrollment_url|
|mam_terms_of_use_url|
|mdm_compliance_url|
|mdm_enrollment_url|
|mdm_terms_of_use_url|
|nameid|
|NBF|
|netbios_name|
|nonce|
|OID|
|on_prem_id|
|onprem_sam_account_name|
|onprem_sid|
|openid2_id|
|password|
|platf|
|polids|
|pop_jwk|
|preferred_username|
|previous_refresh_token|
|primary_sid|
|PUID|
|pwd_exp|
|pwd_url|
|redirect_uri|
|refresh_token|
|refreshtoken|
|request_nonce|
|Kaynak|
|Rolü|
|roles|
|Kapsam|
|SCP|
|SID|
|İmza|
|signin_state|
|src1|
|src2|
|Sub|
|tbid|
|tenant_display_name|
|tenant_region_scope|
|thumbnail_photo|
|komutu|
|tokenAutologonEnabled|
|trustedfordelegation|
|unique_name|
|UPN|
|user_setting_sync_url|
|kullanıcı adı|
|uti|
|ver|
|verified_primary_email|
|verified_secondary_email|
|wids|
|win_ver|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a>Tablo 2: Güvenlik onaylama işlemi biçimlendirme dili (SAML) talep kümesi kısıtlanmış.
|Talep türü (URI)|
| ----- |
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/Expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/Expired|
|http://schemas.microsoft.com/identity/Claims/accesstoken|
|http://schemas.microsoft.com/identity/Claims/openid2_id|
|http://schemas.microsoft.com/identity/Claims/identityprovider|
|http://schemas.microsoft.com/identity/Claims/objectidentifier|
|http://schemas.microsoft.com/identity/Claims/puid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/nameidentifier [MR1] |
|http://schemas.microsoft.com/identity/Claims/tenantid|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/AuthenticationMethod|
|http://schemas.microsoft.com/accesscontrolservice/2010/07/Claims/identityprovider|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/groups|
|http://schemas.microsoft.com/Claims/Groups.Link|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/role|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/wids|
|http://schemas.microsoft.com/2014/09/devicecontext/Claims/iscompliant|
|http://schemas.microsoft.com/2014/02/devicecontext/Claims/isknown|
|http://schemas.microsoft.com/2012/01/devicecontext/Claims/ismanaged|
|http://schemas.microsoft.com/2014/03/psso|
|http://schemas.microsoft.com/Claims/authnmethodsreferences|
|http://schemas.xmlsoap.org/ws/2009/09/identity/Claims/Actor|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/samlissuername|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/confirmationkey|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowsaccountname|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/primarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/primarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/authorizationdecision|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/Authentication|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/Sid|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/denyonlyprimarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/denyonlyprimarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/denyonlysid|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/denyonlywindowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowsdeviceclaim|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowsfqbnversion|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowssubauthority|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/windowsuserclaim|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/x500distinguishedname|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/UPN|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/groupsid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/SPN|
|http://schemas.microsoft.com/ws/2008/06/identity/Claims/ispersistent|
|http://schemas.xmlsoap.org/ws/2005/05/identity/Claims/privatepersonalidentifier|
|http://schemas.microsoft.com/identity/Claims/Scope|

## <a name="claims-mapping-policy-properties"></a>Talep eşleme ilkesi özellikleri
Gelen hello veri burada kaynaklıdır ve hangi taleplerin yayılan İlkesi toocontrol eşleme talep Hello özelliklerini kullanın. Hiçbir ilke ayarlarsanız, hello sistem hello çekirdek talep kümesini içeren belirteçleri, hello temel talep kümesi ve uygulama hello herhangi isteğe bağlı bir talep tooreceive seçilen.

### <a name="include-basic-claim-set"></a>Temel talep kümesi içerir

**Dize:** IncludeBasicClaimSet

**Veri türü:** Boolean (True veya False)

**Özet:** bu özellik bu ilkeden etkilenen belirteçlerinde hello temel talep kümesine dahil edilip edilmeyeceğini belirler. 

- Set tooTrue, hello temel talep kümesindeki tüm talepler hello İlkesi tarafından etkilenen belirteçlerinde gösterilen durumunda. 
- Bunlar ayrı ayrı hello talep şema özelliğinde hello aynı eklenmediği sürece kümesi tooFalse, hello temel talep kümesindeki talepler hello belirteçleri değilse ilkesi.

>[!NOTE] 
>Talep hello çekirdek talepler kümesi bu özelliği ayarlamak bağımsız olarak her belirtecindeki mevcut. 

### <a name="claims-schema"></a>Talep şeması

**Dize:** ClaimsSchema

**Veri türü:** bir veya daha fazla talep şema girişlerle JSON blob

**Özet:** hangi taleplerin hello ilkeden etkilenen hello belirteçleri yok Bu özelliği tanımlar, buna ek olarak toohello temel talep kümesine hem de hello çekirdek talep kümesi.
Bu özelliği içinde tanımlı her talep şema giriş için belirli bilgiler gereklidir. Burada hello veri geldiği belirtmeniz gerekir (**değeri** veya **kaynak/kimliği çifti**), ve hangi hello veri talep olarak gösterilen (**talep türü**).

### <a name="claim-schema-entry-elements"></a>Talep şema girişi öğeleri

**Değer:** hello değeri öğesi hello talep yayılan hello veri toobe olarak statik bir değer tanımlar.

**Kaynak/Kimliği çifti:** kaynak hello ve kimliği öğelerini tanımlama gelen hello talep hello verileri nerede kaynaklıdır. 

Merhaba Source öğesi tooone hello aşağıdaki ayarlamanız gerekir: 


- "kullanıcı": hello hello verileri talep hello kullanıcı nesnesi üzerinde bir özellik. 
- "uygulama": hello hello verileri talep hello uygulama (istemci) hizmet asıl üzerinde bir özellik. 
- "kaynak": hello hello verileri talep hello kaynak hizmet sorumlusu üzerinde bir özellik.
- "İzleyici": hello veri hello talep hello İzleyici hello belirtecinin (ya da hello istemci veya kaynak hizmet sorumlusu) olan hello hizmet sorumlusu üzerinde bir özelliğidir.
- "Şirket": hello hello verileri talep hello kaynak kiracının şirket nesne üzerinde bir özellik.
- "dönüştürmesi": hello hello verileri talep olan talep dönüştürme (Bu makalenin sonraki bölümlerinde hello "talep dönüştürme" bölümüne bakın). 

Merhaba kaynağı dönüştürme ise, hello **TransformationID** öğesi de bu talep tanımını eklenmesi gerekir.

Hangi özelliği hello kaynağı üzerinde hello değer için hello talep sağlar Hello ID öğesi tanımlar. Merhaba aşağıdaki tabloda her bir kaynak değer için geçerli kimlik hello değerleri listeler.

#### <a name="table-3-valid-id-values-per-source"></a>Tablo 3: Kaynak başına geçerli kimlik değeri
|Kaynak|Kimlik|Açıklama|
|-----|-----|-----|
|Kullanıcı|Soyadı|Aile adı|
|Kullanıcı|givenName|Verilen ad|
|Kullanıcı|görünen adı|Görünen ad|
|Kullanıcı|objectID|ObjectID|
|Kullanıcı|Posta|E-posta adresi|
|Kullanıcı|userPrincipalName|Kullanıcı asıl adı|
|Kullanıcı|Bölüm|Bölüm|
|Kullanıcı|onpremisessamaccountname|Şirket içi Sam hesap adı|
|Kullanıcı|netbiosname|NetBIOS adı|
|Kullanıcı|DNSEtkiAlanıAdı|DNS etki alanı adı|
|Kullanıcı|onpremisesecurityidentifier|Şirket içi güvenlik tanımlayıcısı|
|Kullanıcı|Şirket adı|Kuruluş Adı|
|Kullanıcı|streetAddress|Sokak adresi|
|Kullanıcı|posta kodu|Posta kodu|
|Kullanıcı|preferredlanguange|Tercih edilen dili|
|Kullanıcı|onpremisesuserprincipalname|Şirket içi UPN|
|Kullanıcı|mailnickname|Posta takma adı|
|Kullanıcı|extensionattribute1|1 uzantısı özniteliği|
|Kullanıcı|extensionattribute2|Uzantı özniteliği 2|
|Kullanıcı|extensionattribute3|3 uzantısı özniteliği|
|Kullanıcı|extensionattribute4|Uzantı özniteliği 4|
|Kullanıcı|extensionattribute5|Uzantı özniteliği 5|
|Kullanıcı|extensionattribute6|6 uzantısı özniteliği|
|Kullanıcı|extensionattribute7|Uzantı özniteliği 7|
|Kullanıcı|extensionattribute8|Uzantı özniteliği 8|
|Kullanıcı|extensionattribute9|Uzantı özniteliği 9|
|Kullanıcı|extensionattribute10|Uzantı özniteliği 10|
|Kullanıcı|extensionattribute11|Uzantı özniteliği 11|
|Kullanıcı|extensionattribute12|Uzantı özniteliği 12|
|Kullanıcı|extensionattribute13|Uzantı özniteliği 13|
|Kullanıcı|extensionattribute14|Uzantı özniteliği 14|
|Kullanıcı|extensionattribute15|Uzantı özniteliği 15|
|Kullanıcı|othermail|Diğer posta|
|Kullanıcı|Ülke|Ülke|
|Kullanıcı|city|Şehir|
|Kullanıcı|durum|Durum|
|Kullanıcı|İş Unvanı|İş Unvanı|
|Kullanıcı|EmployeeID|Çalışan kimliği|
|Kullanıcı|facsimiletelephonenumber|Faks telefon numarası|
|Uygulama, kaynak, hedef kitle|görünen adı|Görünen ad|
|Uygulama, kaynak, hedef kitle|ait nesneleri|ObjectID|
|Uygulama, kaynak, hedef kitle|etiketler|Hizmet sorumlusu etiketi|
|Şirket|tenantcountry|Kiracının ülke|

**TransformationID:** hello TransformationID öğesi, yalnızca hello Source öğesi çok ayarlanır sağlanan olmalıdır "dönüştürmesi".

- Bu öğe hello ID öğesi hello hello dönüştürme girişinin eşleşmelidir **ClaimsTransformation** hello verileri bu talep için nasıl oluşturulacağını tanımlar özelliği.

**Talep türü:** hello **JwtClaimType** ve **SamlClaimType** öğeleri tanımlamak için bu talep şema giriş başvuruyor talep.

- Merhaba JwtClaimType Jwt'ler içinde gösterilen hello talep toobe hello adını içermelidir.
- Merhaba SamlClaimType hello URI'sini talep SAML belirteçleri yayılan toobe hello içermesi gerekir.

>[!NOTE]
>Adları ve hello Taleplerde URI'ler talep kümesi için hello talep türü öğeleri kullanılamaz kısıtlı. Daha fazla bilgi için bu makalenin sonraki bölümlerinde hello "Özel durumlar ve kısıtlamaları" bölümüne bakın.

### <a name="claims-transformation"></a>Talep dönüştürme

**Dize:** ClaimsTransformation

**Veri türü:** bir veya daha fazla dönüştürme girişlerle JSON blob 

**Özet:** toogenerate hello çıktı verilerini belirtilen talep için talep şema Merhaba, bu özellik tooapply ortak dönüşümleri toosource verileri kullanın.

**Kimliği:** kullanım hello kimliği öğesi tooreference hello TransformationID talep şema girişi bu dönüşüm girişi. Bu değer her dönüştürme giriş Bu ilke içinde benzersiz olması gerekir.

**TransformationMethod:** hello TransformationMethod öğesi tanımlayan gerçekleştirilen toogenerate hello veri hello talep için hangi işlemdir.

Seçilen hello yöntemine bağlı olarak, bir dizi girişleri ve çıkışları beklenir. Bunlar hello kullanılarak tanımlanmış **InputClaims**, **InputParameters** ve **OutputClaims** öğeleri.

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a>Tablo 4: Dönüştürme yöntemleri ve beklenen girişleri ve çıkışları
|TransformationMethod|Beklenen Giriş|Beklenen çıktı|Açıklama|
|-----|-----|-----|-----|
|Birleştir|dize1, dize2, ayırıcı|outputClaim|Birleşimler, ayırıcı arasında kullanarak dizeleri girin. Örneğin: Dize1: "foo@bar.com", dize2: "korumalı alan", ayırıcı: "." sonuçları içinde outputClaim: "foo@bar.com.sandbox"|
|ExtractMailPrefix|Posta|outputClaim|Bir e-posta adresi yerel parçası Hello ayıklar. Örneğin: posta: "foo@bar.com" sonuçları içinde outputClaim: "foo". Merhaba orignal giriş dizesi olarak döndürülür Hayır @ işareti varsa, ise.|

**InputClaims:** bir InputClaims öğesi toopass hello verilerden bir talep şema girişi tooa dönüştürmeyi kullanın. İki özniteliklere sahiptir: **ClaimTypeReferenceId** ve **TransformationClaimType**.

- **ClaimTypeReferenceId** hello talep şema girişi toofind hello uygun giriş talep kimliği öğesi ile birleştirilir. 
- **TransformationClaimType** kullanılan toogive benzersiz bir ad toothis giriş olabilir. Bu ad hello dönüştürme yöntemi beklenen hello girdileri eşleşmelidir.

**InputParameters:** InputParameters öğesi toopass bir sabit değer tooa dönüştürmesi kullanın. İki özniteliklere sahiptir: **değeri** ve **kimliği**.

- **Değer** hello gerçek sabit değer toobe geçirilir.
- **Kimliği** kullanılan toogive benzersiz bir ad toothis giriş olabilir. Bu ad hello dönüştürme yöntemi beklenen hello girdileri eşleşmelidir.

**OutputClaims:** tooa talep şema girişi tie ve bir dönüşüm tarafından oluşturulan bir OutputClaims öğe toohold hello verileri kullanın. İki özniteliklere sahiptir: **ClaimTypeReferenceId** ve **TransformationClaimType**.

- **ClaimTypeReferenceId** hello talep şema girişi toofind hello uygun çıkış talep hello kimliği ile birleştirilir.
- **TransformationClaimType** kullanılan toogive benzersiz bir ad toothis çıkış alınır. Bu ad hello dönüştürme yöntemi beklenen hello çıktıların biriyle eşleşmelidir.

### <a name="exceptions-and-restrictions"></a>Özel durumlar ve kısıtlamaları

**SAML NameID ve UPN:** içinden hello NameID ve UPN değerleri kaynağı ve hello talep izin verilen dönüşümleri hello öznitelikleri sınırlıdır.

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a>Tablo 5: bir veri kaynağı olarak SAML NameID için izin verilen öznitelikleri
|Kaynak|Kimlik|Açıklama|
|-----|-----|-----|
|Kullanıcı|Posta|E-posta adresi|
|Kullanıcı|userPrincipalName|Kullanıcı asıl adı|
|Kullanıcı|onpremisessamaccountname|Şirket içi Sam hesap adı|
|Kullanıcı|EmployeeID|Çalışan kimliği|
|Kullanıcı|extensionattribute1|1 uzantısı özniteliği|
|Kullanıcı|extensionattribute2|Uzantı özniteliği 2|
|Kullanıcı|extensionattribute3|3 uzantısı özniteliği|
|Kullanıcı|extensionattribute4|Uzantı özniteliği 4|
|Kullanıcı|extensionattribute5|Uzantı özniteliği 5|
|Kullanıcı|extensionattribute6|6 uzantısı özniteliği|
|Kullanıcı|extensionattribute7|Uzantı özniteliği 7|
|Kullanıcı|extensionattribute8|Uzantı özniteliği 8|
|Kullanıcı|extensionattribute9|Uzantı özniteliği 9|
|Kullanıcı|extensionattribute10|Uzantı özniteliği 10|
|Kullanıcı|extensionattribute11|Uzantı özniteliği 11|
|Kullanıcı|extensionattribute12|Uzantı özniteliği 12|
|Kullanıcı|extensionattribute13|Uzantı özniteliği 13|
|Kullanıcı|extensionattribute14|Uzantı özniteliği 14|
|Kullanıcı|extensionattribute15|Uzantı özniteliği 15|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a>Tablo 6: SAML NameID için izin verilen dönüştürme yöntemleri
|TransformationMethod|Kısıtlamaları|
| ----- | ----- |
|ExtractMailPrefix|None|
|Birleştir|Birleştirilen hello soneki doğrulanmış bir etki alanı hello kaynak Kiracı olmalıdır.|

### <a name="custom-signing-key"></a>Özel anahtar imzalama
Özel bir imzalama anahtarı toohello hizmet sorumlusu nesnesi İlkesi tootake etkisi eşleme talepler için atanmış olması gerekir. Hello İlkesi tarafından etkilenip etkilenmediğinizi yayınlanan tüm belirteçleri bu anahtarla imzalanmıştır. Uygulamalar, bu anahtarı ile imzalanmış yapılandırılmış tooaccept belirteçleri olmalıdır. Bu eşleme ilkesi belirteçleri hello hello oluşturucusu tarafından değiştirildiğini bildirim talep sağlar. Bu uygulamaları kötü amaçlı aktörler tarafından oluşturulan ilkeler eşleme talep önler.

### <a name="cross-tenant-scenarios"></a>Çapraz Kiracı senaryoları
Talep eşleme ilkeleri tooguest kullanıcılara uygulanmaz. Konuk kullanıcı bir uygulama tooaccess çalışırsa ile bir talep eşleme atanan ilke tooits asıl hizmet, hello varsayılan belirteci verildiği (hello İlkesi etkisi yoktur).

## <a name="claims-mapping-policy-assignment"></a>İlke ataması eşleme talepleri
Talep eşleme ilkeleri yalnızca tooservice asıl nesneleri atanabilir.

### <a name="example-claims-mapping-policies"></a>Örnek eşleme ilkeleri talepleri

Azure AD'de belirteçleri belirli hizmet asıl adı için gösterilen talep özelleştirdiğinizde birçok senaryo mümkündür. Bu bölümde, nasıl toouse hello eşleme ilke türü talep kavramak yardımcı olabilecek bazı yaygın senaryolar üzerinden yol.

#### <a name="prerequisites"></a>Ön koşullar
Merhaba, örnek olarak oluşturmak, güncelleştirme, bağlantı ve ilkelerini için hizmet asıl adı silin. Yeni tooAzure AD varsa, Azure AD bir tooget nasıl Kiracı bu örnekleri ile devam etmeden önce hakkında bilgi edinin öneririz. 

başlatıldı, tooget hello adımları izleyin:


1. Merhaba son karşıdan [Azure AD PowerShell modülü genel Önizleme sürümü](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).
2.  Merhaba Bağlan komutu toosign tooyour Azure AD yönetim hesabı çalıştırın. Her zaman bu komutu çalıştırmak yeni bir oturum başlatın.
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  toosee kuruluşunuzda aşağıdaki çalışma hello oluşturulan tüm ilkeler komutu. Merhaba, çoğu işlemlerinden sonra bu komutu çalıştırmanızı öneririz senaryoları ilkelerinizi olarak oluşturulan toocheck bekleniyor.
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a>Örnek: Oluşturun ve verilen belirteçleri tooa hizmet sorumlusu bir ilke tooomit hello temel talepleri atayın.
Bu örnekte, hizmet asıl adı hello temel talep kümesi yayınlanan belirteçleri toolinked kaldıran bir ilke oluşturun.


1. İlke eşleme bir talep oluşturmak. Bu ilke, bağlantılı toospecific hizmet asıl adı gelen belirteçleri hello temel talep kümesi kaldırır.
    1. toocreate hello İlkesi, bu komutu çalıştırın: 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. Yeni ilke ve tooget hello İlkesi objectID, aşağıdaki çalışma hello komutu toosee:
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Hello İlkesi tooyour hizmet sorumlusu atayın. Ayrıca tooget hello hizmet sorumlusu objectID gerekir. 
    1.  toosee kuruluşunuzun tüm hizmet asıl adı, Microsoft Graph sorgulayabilirsiniz. Veya Azure AD Graph Explorer'da tooyour Azure AD hesabının oturum açın.
    2.  Merhaba, hizmet asıl, çalıştırma komutu aşağıdaki hello objectID varsa:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a>Örnek: Oluşturmak ve bir ilke tooinclude atamak belirteçleri Taleplerde tooa hizmet sorumlusu verildiğinde EmployeeID ve TenantCountry hello.
Bu örnekte, hello EmployeeID ekler bir ilke oluşturun ve TenantCountry tootokens toolinked hizmet asıl adı verilen. Merhaba EmployeeID SAML belirteçleri ve Jwt'ler hello adı talep türü olarak yayılır. Merhaba ülke talebi olarak SAML belirteçleri ve Jwt'ler türü hello TenantCountry yayınlanır. Bu örnekte, tooinclude hello temel talep hello belirteçleri ayarlama devam ediyoruz.

1. İlke eşleme bir talep oluşturmak. Bu ilke, bağlantılı toospecific hizmet asıl adı, hello EmployeeID ve TenantCountry talep tootokens ekler.
    1. toocreate hello İlkesi, bu komutu çalıştırın:  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. Yeni ilke ve tooget hello İlkesi objectID, aşağıdaki çalışma hello komutu toosee:
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  Hello İlkesi tooyour hizmet sorumlusu atayın. Ayrıca tooget hello hizmet sorumlusu objectID gerekir. 
    1.  toosee kuruluşunuzun tüm hizmet asıl adı, Microsoft Graph sorgulayabilirsiniz. Veya Azure AD Graph Explorer'da tooyour Azure AD hesabının oturum açın.
    2.  Merhaba, hizmet asıl, çalıştırma komutu aşağıdaki hello objectID varsa:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a>Örnek: Oluşturun ve asıl yayınlanan belirteçleri tooa hizmetinde bir talep dönüştürme kullanan bir ilke atayın.
Bu örnekte, tooJWTs toolinked hizmet asıl adı verilen bir özel talep "JoinedData" yayar bir ilke oluşturun. Bu talep hello extensionattribute1 özniteliği ".sandbox" ile Merhaba kullanıcı nesnesinde depolanan hello veri birleştirilmesiyle oluşturulan bir değer içeriyor. Bu örnekte, hello temel talep hello belirteçleri ayarlamak dışlayın.


1. İlke eşleme bir talep oluşturmak. Bu ilke, bağlantılı toospecific hizmet asıl adı, hello EmployeeID ve TenantCountry talep tootokens ekler.
    1. toocreate hello İlkesi, bu komutu çalıştırın: 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. Yeni ilke ve tooget hello İlkesi objectID, aşağıdaki çalışma hello komutu toosee: 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Hello İlkesi tooyour hizmet sorumlusu atayın. Ayrıca tooget hello hizmet sorumlusu objectID gerekir. 
    1.  toosee kuruluşunuzun tüm hizmet asıl adı, Microsoft Graph sorgulayabilirsiniz. Veya Azure AD Graph Explorer'da tooyour Azure AD hesabının oturum açın.
    2.  Merhaba, hizmet asıl, çalıştırma komutu aşağıdaki hello objectID varsa: 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
