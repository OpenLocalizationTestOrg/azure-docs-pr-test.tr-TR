---
title: "etki alanına katılmış Windows cihazlarının Azure Active Directory ile aaaHow tooconfigure otomatik kayıt | Microsoft Docs"
description: "Etki alanına katılmış Windows cihazları tooregister, Azure Active Directory ile otomatik olarak ve sessiz bir şekilde ayarlayın."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a>Nasıl tooconfigure otomatik kayıt Windows etki alanına katılmış cihazları Azure Active Directory ile

toouse [Azure Active Directory cihaz temelli koşullu erişim](active-directory-conditional-access-azure-portal.md), bilgisayarlarınızı Azure Active Directory (Azure AD) ile kayıtlı olması gerekir. Hello kullanarak kuruluşunuzdaki kayıtlı aygıtların listesini alabilirsiniz [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) hello cmdlet'te [Azure Active Directory PowerShell Modülü](/powershell/azure/install-msonlinev1?view=azureadps-2.0). 

Bu makale, kuruluşunuzda Azure AD ile etki alanına katılmış Windows cihazlarının hello otomatik kaydını yapılandırmak için ile Merhaba adımları sağlar.


Hakkında daha fazla bilgi için:

- Koşullu erişim bkz [Azure Active Directory cihaz temelli koşullu erişim](active-directory-conditional-access-azure-portal.md). 
- Windows 10 cihazları hello çalışma alanına ve Azure AD ile kaydolurken hello geliştirilmiş deneyimler görmek [hello kuruluş için Windows 10: cihazları iş için kullanmak](active-directory-azureadjoin-windows10-devices-overview.md).
- Windows 10 Kurumsal E3 CSP içinde bkz hello [Windows 10 Kurumsal E3 CSP genel bakış](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).


## <a name="before-you-begin"></a>Başlamadan önce

Ortamınızda Windows etki alanına katılmış cihazların Merhaba otomatik kayıt yapılandırmaya başlamadan önce kendiniz hello desteklenen senaryolar ve hello kısıtlamaları kazanmalısınız.  

Merhaba okunabilirliğini hello açıklamaları tooimprove, bu konuda terim aşağıdaki hello kullanır: 

- **Windows geçerli aygıtları** -Windows 10 veya Windows Server 2016 çalıştıran toodomain katılmış cihazlarda bu terimi anlamına gelir.
- **Windows alt düzey aygıtları** -bu terim tooall başvuruyor **desteklenen** çalışan Windows 10 ne Windows Server 2016 etki alanına katılmış Windows cihazları.  


### <a name="windows-current-devices"></a>Geçerli Windows cihazları

- Merhaba Windows masaüstü işletim sistemi çalıştıran cihazlar için Windows 10 Anniversary güncelleştirme (sürüm 1607) kullanılmasını öneririz veya sonraki bir sürümü. 
- Merhaba geçerli Windows cihazlarının kaydı **olan** parola karma eşitlemesi yapılandırmaları gibi Federasyon olmayan ortamlarda desteklenir.  


### <a name="windows-down-level-devices"></a>Windows alt düzey aygıtları

- Windows alt düzey aygıtları aşağıdaki hello desteklenir:
    - Windows 8.1
    - Windows 7
    - Windows Server 2012 R2
    - Windows Server 2012
    - Windows Server 2008 R2
- Merhaba Windows alt düzey cihazlarının kaydı **olan** sorunsuz çoklu oturum açma ile federe olmayan ortamlarda desteklenen [Azure Active Directory sorunsuz çoklu oturum açma](https://aka.ms/hybrid/sso).
- Merhaba Windows alt düzey cihazlarının kaydı **değil** dolaşım profilleri kullanarak cihazları için desteklenir. Dolaşım profilleri veya ayarlarını FQDN'yi kullanıyorsanız, Windows 10 kullanın.



## <a name="prerequisites"></a>Ön koşullar

Etki alanına katılmış cihazların kuruluşunuzdaki hello otomatik kaydı etkinleştirme başlamadan önce Azure AD güncel bir sürümünü çalıştırdığından emin toomake gerekir bağlanın.

Azure AD Connect:

- Şirket içi Active Directory (AD) ve Azure AD'de hello cihaz nesnesi hello bilgisayar hesabını arasındaki ilişkiyi Hello tutar. 
- Başka bir aygıt etkinleştirir ilgili özellikler gibi iş için Windows Hello.



## <a name="configuration-steps"></a>Yapılandırma adımları

Bu konuda, tüm normal yapılandırma senaryoları için gerekli hello adımlarını içerir.  
Aşağıdaki tablo tooget senaryonuz için gerekli olan hello adımlara genel bir bakış hello kullan:  



| Adımlar                                      | Windows geçerli ve parola karma eşitlemesi | Windows geçerli ve Federasyon | Alt düzey Windows |
| :--                                        | :-:                                    | :-:                            | :-:                |
| 1. adım: hizmet bağlantı noktası yapılandırma | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |
| 2. adım: talep verme kurma           |                                        | ![İşaretli][1]                    | ![İşaretli][1]        |
| 3. adım: Windows 10 cihazları etkinleştirme      |                                        |                                | ![İşaretli][1]        |
| Adım 4: Denetimi dağıtımı ve dağıtım     | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |
| 5. adım: kayıtlı cihazlar doğrulayın          | ![İşaretli][1]                            | ![İşaretli][1]                    | ![İşaretli][1]        |



## <a name="step-1-configure-service-connection-point"></a>1. adım: hizmet bağlantı noktası yapılandırma

Merhaba hizmet bağlantı noktası (SCP) nesnesinin hello kayıt toodiscover sırasında Azure AD Kiracı bilgilerini cihazlar tarafından kullanılır. Şirket içi Active Directory (AD), etki alanına katılmış cihazların Merhaba otomatik kaydı için hello SCP nesnesi hello yapılandırma adlandırma bağlamı bölümünde hello bilgisayarın orman mevcut olmalıdır. Her ormanda yalnızca bir yapılandırma adlandırma bağlamında yoktur. Bir Çoklu orman Active Directory yapılandırması, etki alanına katılmış bilgisayarları içeren tüm ormanlarda hello hizmet bağlantı noktası mevcut olmalıdır.

Merhaba kullanabilirsiniz [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello yapılandırma adlandırma bağlamında ormanınızın.  

Merhaba Active Directory etki alanı adına sahip bir orman için *fabrikam.com*, hello yapılandırma adlandırma bağlamında değil:

`CN=Configuration,DC=fabrikam,DC=com`

Ormanınıza hello otomatik kaydı etki alanına katılmış cihazlar için hello SCP nesnesi şu konumdadır:  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

Nasıl Azure AD Connect dağıttığınız bağlı olarak, hello SCP nesnesi zaten yapılandırılmış olabilir.
Hello nesne hello varlığını doğrulayın ve Windows PowerShell Betiği aşağıdaki hello kullanarak hello bulma değerleri alabilirsiniz: 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

Merhaba **$scp. Anahtar sözcükler** çıktı hello Azure AD Kiracı bilgileri, örneğin gösterir:

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

Merhaba hizmet bağlantı noktası mevcut değilse, bunu hello çalıştırarak oluşturabilirsiniz `Initialize-ADSyncDomainJoinedComputerSync` Azure AD Connect sunucunuzda cmdlet'i. Kuruluş yönetici kimlik bilgileri gerekli toorun bu cmdlet'tir.  
Merhaba cmdlet:

- Azure AD Connect bağlı hello Active Directory ormanındaki Hello hizmet bağlantı noktası oluşturur. 
- Toospecify hello gerektirir `AdConnectorAccount` parametresi. Active Directory Bağlayıcısı hesabı Azure ad connect yapılandırılmış hello hesap budur. 


Merhaba aşağıdaki komut dosyası hello cmdlet'ini kullanarak bir örnek gösterilmektedir. Bu komut `$aadAdminCred = Get-Credential` tootype bir kullanıcı adı gerektirir. Merhaba kullanıcı asıl adı (UPN) biçiminde tooprovide hello kullanıcı adı gerekir (`user@example.com`). 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

Merhaba `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:

- Bir etki alanı denetleyicisinde çalışan Active Directory Web Hizmetleri dayanan hello Active Directory PowerShell modülü kullanır. Active Directory Web Hizmetleri, Windows Server 2008 R2 çalıştıran etki alanı denetleyicilerinde ve üzerinde desteklenir.
- Yalnızca hello tarafından desteklenen **MSOnline PowerShell modülü sürümü 1.1.166.0**. toodownload bu modül bu [bağlantı](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).   

Windows Server 2008 veya önceki sürümlerini çalıştıran etki alanı denetleyicileri için toocreate hello hizmet bağlantı noktası aşağıdaki hello komut dosyası kullanın.

Bir Çoklu orman yapılandırması, komut dosyası toocreate hello hizmet bağlantı noktası bilgisayarları var olduğu her bir orman içinde aşağıdaki hello kullanmanız gerekir:
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a>2. adım: talep verme kurma

Bir Federasyon Azure AD yapılandırma cihazlar Active Directory Federasyon Hizmetleri (AD FS) üzerinde kullanır veya 3. taraf bir Federasyon Hizmeti tooauthenticate tooAzure AD şirket içi. Aygıtları tooget bir erişim belirteci tooregister hello Azure Active Directory cihaz kayıt Hizmeti'ne (Azure DRS) karşı kimlik doğrulaması.

Windows hello şirket içi Federasyon Hizmeti tarafından barındırılan tümleşik Windows kimlik doğrulaması tooan etkin WS-Trust uç noktası (1.3 veya 2005 sürümler) kullanarak geçerli aygıtların kimlik doğrulaması.

> [!NOTE]
> AD FS, ya da kullanırken **adfs/services/güven/13/windowstransport** veya **adfs/services/güven/2005/windowstransport** etkinleştirilmesi gerekir. Ayrıca hello Web kimlik doğrulaması Proxy kullanıyorsanız, bu uç noktaya hello proxy üzerinden yayımlanan emin olun. Hangi uç noktalarının altında hello AD FS Yönetim Konsolu aracılığıyla özelliğinin etkinleştirilip etkinleştirilmediğini **hizmet > uç noktaları**.
>
>AD FS, şirket içi Federasyon Hizmeti olarak yoksa, WS-Trust 1.3 veya 2005 uç noktalarının ve bunlar hello meta veri değişimi dosya (MEX) yayımlanır desteklediğinden emin, satıcı toomake hello yönergeleri izleyin.

Merhaba aşağıdaki talep için cihaz kayıt toocomplete Azure DRS tarafından alınan hello belirtecindeki mevcut olması gerekir. Azure DRS Azure AD ile sonra Azure AD Connect tooassociate yeni oluşturulan hello cihaz nesnesi hello bilgisayar hesabı şirket tarafından kullanılan bu bilgilerin bazıları, bir cihaz nesnesi oluşturun.

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

Birden fazla doğrulanan etki alanı adı varsa, talep bilgisayarlar için aşağıdaki tooprovide hello gerekir:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

Zaten bir İmmutableıd talep (örn., alternatif oturum açma kimliği) dağıttığınız bilgisayarlar için bir karşılık gelen talep tooprovide gerekir:

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

Aşağıdaki bölümlerde hello hakkında bilgiler yer:
 
- Merhaba değerleri her talep olmalıdır
- Nasıl bir tanımı gibi AD FS'de görüneceği

Merhaba tanımı yardımcı olan tooverify hello değerleri mevcut olup olmadığını veya toocreate ihtiyacınız varsa, bunları.

> [!NOTE]
> Şirket içi Federasyon sunucunuz için AD FS kullanmıyorsanız, bu talepler satıcınızın yönergeleri toocreate hello uygun yapılandırma tooissue izleyin.

### <a name="issue-account-type-claim"></a>Sorunu hesap türü talep

**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Bu talep değerini içermelidir **DJ**, hello cihaz etki alanına katılmış bir bilgisayar olarak tanımlar. AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a>Sorunu objectGUID hello bilgisayar hesabı şirket içinde

**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Bu talep hello içermelidir **objectGUID** hello değerini şirket içi bilgisayar hesabı. AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a>Sorunu objectSID hello bilgisayar hesabı şirket içinde

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Bu talep hello hello içermelidir **objectSID** hello değerini şirket içi bilgisayar hesabı. AD FS'de şuna benzer bir verme dönüştürme kural ekleyebilirsiniz:

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a>Birden çok etki alanı adlarını Azure AD'de belirlediğinizde issuerID bilgisayar için sorun

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Bu talep hello hiçbirinin Tekdüzen Kaynak Tanımlayıcısı (URI) ile Merhaba bağlanmak etki alanı adları şirket içi Federasyon Hizmeti (AD FS veya 3. taraf) sertifika veren hello belirteci doğrulandı hello içermesi gerekir. AD FS içinde sonra belirli bir sıraya Merhaba, olanları yukarıdaki olanları aşağıdaki hello gibi görünmesini verme dönüştürme kuralları ekleyebilirsiniz. Lütfen gerekli kullanıcılar için bir kural tooexplicitly sorunu hello kural unutmayın. Merhaba kuralları'nda aşağıdaki kullanıcı ve bilgisayar kimlik doğrulaması tanımlama ilk bir kuralı eklenir.

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


Yukarıdaki Hello talep kümesinde

- `$<domain>`Merhaba AD FS hizmet URL'si
- `<verified-domain-name>`tooreplace doğrulanmış etki alanı adlarınızı biri ile Azure AD içinde gereksinim duyduğunuz bir yer tutucudur



Doğrulanmış etki alanı adları hakkında daha fazla ayrıntı için bkz: [özel etki alanı adı tooAzure Active Directory eklemek](active-directory-add-domain.md).  
tooget doğrulanmış şirket etki alanlarının bir listesini, kullanabileceğiniz hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet'i. 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a>Kullanıcılar için bir tane bulunduğunda (kimliği ayarlanmadan örneğin alternatif oturum açma) İmmutableıd bilgisayar için sorun

**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**-Bu talep bilgisayarlar için geçerli bir değer içermesi gerekir. AD FS içinde verme dönüştürme kural aşağıdaki gibi oluşturabilirsiniz:

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a>Yardımcı betik toocreate hello AD FS verme dönüştürme kuralları

Merhaba aşağıdaki betiği hello verme hello oluşturulmasını ile yukarıda açıklanan kuralları dönüştürme yardımcı olur.

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a>Açıklamalar 

- Bu komut dosyası hello kuralları toohello mevcut kurallar ekler. Merhaba kuralları ayarlamak için çalışmıyor hello betik iki kez iki kez eklenir. Karşılık gelen hiçbir kural (koşullarda hello karşılık gelen) bu talepler için hello betiği yeniden çalıştırmadan önce var olduğundan emin olun.

- Merhaba değerini ayarlayın (hello Azure AD portalında veya hello Get-MsolDomains cmdlet'i aracılığıyla gösterildiği gibi) birden çok doğrulanmış etki alanı adı, varsa **$multipleVerifiedDomainNames** hello çok komut dosyası**$true**. Ayrıca Azure AD Connect veya başka yöntemler aracılığıyla oluşturulan tüm mevcut issuerid talep kaldırdığınızdan emin olun. Bu kural için örnek aşağıda verilmiştir:


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- Zaten yayımlandı durumunda bir **İmmutableıd** hello değeri olarak ayarlayın, kullanıcı hesapları için talep **$immutableIDAlreadyIssuedforUsers** hello çok komut dosyası**$true**.

## <a name="step-3-enable-windows-down-level-devices"></a>Adım 3: Windows alt düzey aygıtları etkinleştirin

Bazı etki alanına katılmış aygıtlarınız Windows cihazları sürümlerdeki, gerekir:

- Bir ilke Azure AD tooenable kullanıcılar tooregister aygıtları ayarlayın.
 
- Şirket içi Federasyon Hizmeti tooissue talep toosupport yapılandırma **tümleşik Windows kimlik doğrulaması (IWA)** cihaz kaydı için.
 
- Merhaba aygıt doğrulanırken tooavoid sertifika ister hello Azure AD cihaz kimlik doğrulama uç noktası toohello yerel Intranet bölgeler ekleyin.

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a>İlke Azure AD tooenable kullanıcılar tooregister aygıtları ayarlayın.

tooregister Windows alt düzey aygıtları toomake tooallow kullanıcılar Azure AD'de tooregister cihazları ayarlama bu hello ayarlandığından emin gerekir. Hello Azure portalı, bu ayarı altında bulabilirsiniz:

`Azure Active Directory > Users and groups > Device settings`
    
Merhaba aşağıdaki İlkesi çok ayarlanmalıdır**tüm**: **kullanıcıları Azure AD ile cihazlarını kaydetme**

![Cihaz kaydetme](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a>Şirket içi Federasyon hizmetini yapılandır 

Şirket içi Federasyon hizmetinizi veren hello desteklemelidir **authenticationmehod** ve **wiaormultiauthn** bir kimlik doğrulama alırken talep isteği toohello Azure AD bağlı olan taraf bulunduran bir resouce_params parametre gösterildiği gibi kodlanmış bir değeri olan aşağıdaki:

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

Böyle bir istek geldiğinde, hello şirket içi Federasyon Hizmeti tümleşik Windows kimlik doğrulaması kullanarak hello kullanıcı kimlik doğrulaması yapmalıdır ve başarı iki talep aşağıdaki hello kesmeniz gerekir:

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

AD FS içinde verme dönüştürme kural bu geçişleri üzerinden hello kimlik doğrulama yöntemi eklemeniz gerekir.  

**tooadd bu kural:**

1. Merhaba AD FS yönetim konsolunda çok Git`AD FS > Trust Relationships > Relying Party Trusts`.
2. Merhaba Microsoft Office 365 kimlik Platformu'na bağlı taraf güven nesnesi sağ tıklayın ve ardından **talep kurallarını Düzenle**.
3. Merhaba üzerinde **verme dönüştürme kuralları** sekmesine **Kuralı Ekle**.
4. Merhaba, **talep kuralı** şablonu listesinden **talepleri özel kural kullanarak Gönder**.
5. Seçin **sonraki**.
6. Merhaba, **talep kuralı adı** kutusuna **kimlik doğrulama yöntemi talep kuralı**.
7. Merhaba, **talep kuralı** kutusu, aşağıdaki kural türü hello:

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. Değiştirildikten sonra Federasyon sunucunuzda aşağıdaki hello PowerShell komutunu yazın  **\<RPObjectName\>**  hello bağlı olan taraf için nesne adı, Azure AD bağlı olan taraf güven nesnesi ile. Bu nesne genellikle adlı **Microsoft Office 365 kimlik Platformu'na**.
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a>Hello Azure AD cihaz kimlik doğrulama uç noktası toohello yerel Intranet bölgeler ekleyin

tooAzure Internet Explorer'da URL toohello yerel Intranet bölgesine izleyen bir ilke tooyour etki alanına katılmış aygıtlar tooadd hello gönderebilir AD kaydı cihazları kullanıcıların kimliğini doğrularken tooavoid sertifika ister:

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a>Adım 4: Denetimi dağıtımı ve dağıtım

Merhaba gerekli adımları tamamladıktan sonra etki alanına katılmış hazır tooautomatically kayıt Azure AD ile aygıtlardır. Windows 10 Anniversary güncelleştirmesi ve Windows Server 2016 çalıştıran tüm etki alanına katılmış cihazlar otomatik olarak kayıt aygıt adresindeki Azure AD ile yeniden başlatın veya kullanıcı oturum açma. Yeni cihazların Merhaba etki alanına katılma işlemi tamamlandıktan sonra hello aygıt yeniden başlatıldığında Azure AD ile kaydedin.

Daha önce çalışma alanına katılmış tooAzure AD (örneğin Intune) geçişi çok olan cihaz"*etki alanına katılmış, AAD kayıtlı*"; Ancak, gereken süre bu işlem toocomplete için toohello normal son tüm cihazlar arasında etki alanı ve kullanıcı etkinliğini akışı.

### <a name="remarks"></a>Açıklamalar

- Windows 10 ve Windows Server 2016 etki alanına katılmış bilgisayarlar otomatik kaydını bir Grup İlkesi nesnesi toocontrol hello sunumu kullanabilirsiniz.

- Windows 10 Kasım 2015 güncelleştirmesi otomatik olarak yazmaçlar Azure AD ile **yalnızca** hello sunum Grup İlkesi nesnesi ayarlarsanız.

- dağıtabileceğiniz Windows alt düzey bilgisayarların toorollout hello otomatik kayıt, bir [Windows Installer paketi](#windows-installer-packages-for-non-windows-10-computers) seçtiğiniz toocomputers.

- Merhaba Grup İlkesi nesnesi tooWindows 8.1 etki alanına katılmış aygıtlar itme, kayıt denenecek; Ancak, hello kullanmanız önerilir [Windows Installer paketi](#windows-installer-packages-for-non-windows-10-computers) tooregister tüm Windows alt düzey cihazlar. 

### <a name="create-a-group-policy-object"></a>Bir Grup İlkesi nesnesi oluşturma 

toocontrol hello sunum otomatik kayıt geçerli bilgisayarların Windows hello dağıtmalısınız **etki alanına katılmış bilgisayarları cihaz olarak kaydetme** tooregister istediğiniz Grup İlkesi nesnesi toohello aygıtlar. Örneğin, hello İlkesi tooan kuruluş birimi ya da tooa güvenlik grubu dağıtabilirsiniz.

**tooset hello İlkesi:**

1. Açık **Sunucu Yöneticisi'ni**ve çok Git`Tools > Group Policy Management`.
2. Windows geçerli bilgisayarların tooactivate otomatik kaydı istediğiniz toohello etki alanı karşılık gelen toohello etki alanı düğümüne gidin.
3. Sağ **Grup İlkesi nesneleri**ve ardından **yeni**.
4. Grup İlkesi nesnesi için bir ad yazın. Örneğin, *otomatik kayıt tooAzure AD*. **Tamam**’ı seçin.
5. Yeni Grup İlkesi nesneniz sağ tıklayın ve ardından **Düzenle**.
6. Çok Git**Bilgisayar Yapılandırması** > **ilkeleri** > **Yönetim Şablonları** > **Windows Bileşenleri** > **aygıt kaydı**. Sağ **etki alanına katılmış bilgisayarları cihaz olarak kaydetme**ve ardından **Düzenle**.
   
   > [!NOTE]
   > Bu Grup İlkesi şablonu hello Grup İlkesi Yönetimi konsolunun önceki sürümlerden adlandırıldı. Merhaba konsol önceki bir sürümünü kullanıyorsanız, çok Git`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`. 

7. Seçin **etkin**ve ardından **Uygula**.
8. **Tamam**’ı seçin.
9. Bağlantı hello Grup İlkesi nesnesi tooa konum. Örneğin, tooa belirli bir kuruluş birimine bağlantı oluşturabilirsiniz. Ayrıca Azure AD ile otomatik olarak kaydedilecek bilgisayarların tooa belirli bir güvenlik grubu bağlayabilirsiniz. tooset Bu ilke tüm etki alanına katılmış Windows 10 ve Windows Server 2016 kuruluşunuzdaki bilgisayarların, bağlantı hello Grup İlkesi nesnesi toohello etki alanı için.

### <a name="windows-installer-packages-for-non-windows-10-computers"></a>Windows 10 bilgisayarları için Windows Installer paketleri

tooregister etki alanına katılmış Windows alt düzey bilgisayarları Federasyon ortamında, indirin ve bu Windows Installer (.msi) paketi İndirme Merkezi'nden hello yükleyin [Microsoft çalışma alanına katılma için Windows 10 bilgisayarları](https://www.microsoft.com/en-us/download/details.aspx?id=53554) sayfası.

Bir yazılım dağıtım sistemi gibi System Center Configuration Manager kullanılarak hello paketi dağıtabilirsiniz. Merhaba paketi destekler hello hello standart sessiz yükleme seçenekleriyle *sessiz* parametresi. System Center Configuration Manager geçerli dalının hello özelliği tamamlandı tootrack kayıtlar gibi önceki sürümlerinden ek avantajlar sunar. Daha fazla bilgi için bkz: [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).

Hello yükleyici hello sistemde hello kullanıcının bağlamında çalışan zamanlanmış bir görev oluşturur. içinde tooWindows Hello kullanıcı oturum açtığında hello görevi tetiklenir. Başlangıç görevi hello aygıt hello kullanıcı kimlik bilgileriyle tümleşik Windows kimlik doğrulaması kullanarak kimlik doğrulama sonra Azure AD ile sessizce kaydeder. toosee hello zamanlanan görev hello aygıtta Git çok**Microsoft** > **çalışma alanına katılma**, ve ardından toohello Görev Zamanlayıcı Kitaplığı gidin.

## <a name="step-5-verify-registered-devices"></a>5. adım: kayıtlı cihazlar doğrulayın

Hello kullanarak, kuruluşunuzda başarılı kayıtlı cihazlar denetleyebilirsiniz [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) hello cmdlet'te [Azure Active Directory PowerShell Modülü](/powershell/azure/install-msonlinev1?view=azureadps-2.0).

Merhaba bu cmdlet'in çıktısı, Azure AD'de kayıtlı cihazları gösterir. tooget, tüm cihazların Merhaba kullanmak **-tüm** parametre ve filtre hello kullanarak bunları **deviceTrustType** özelliği. Etki alanına katılmış aygıtlar değerine sahip **etki alanına katılmış**.

## <a name="next-steps"></a>Sonraki adımlar

* [Otomatik cihaz kaydı SSS](active-directory-device-registration-faq.md)
* [Birleştirilmiş bilgisayarlar tooAzure AD – Windows 10 ve Windows Server 2016 etki alanının otomatik kayıt sorunlarını giderme](active-directory-device-registration-troubleshoot-windows.md)
* [Birleştirilmiş bilgisayarlar tooAzure AD – Windows 10 etki alanının otomatik kayıt sorunlarını giderme](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [Azure Active Directory koşullu erişimi](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
