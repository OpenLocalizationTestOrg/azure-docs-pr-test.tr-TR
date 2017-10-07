---
title: "aaaActive Directory Federasyon Hizmetleri Yönetimi ve Azure AD Connect ile özelleştirme | Microsoft Docs"
description: "Azure AD Connect ve AD FS oturum açma ile kullanıcı deneyimi Azure AD Connect ve PowerShell özelleştirmesini ile AD FS yönetimi."
keywords: "AD FS, ADFS, AD FS yönetimi, AAD bağlanma, bağlan, oturum açma, AD FS özelleştirmesi, onarım güven, O365, Federasyon, bağlı olan taraf"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a>Yönetmek ve Azure AD Connect kullanarak Active Directory Federasyon Hizmetleri özelleştirme
Bu makalede nasıl toomanage ve Azure Active Directory (Azure AD) Bağlan kullanarak Active Directory Federasyon Hizmetleri (AD FS) özelleştirin. Ayrıca, bir AD FS grubu için bir tam yapılandırma toodo gerekebilecek diğer ortak AD FS görevler içerir.

| Konu | Ne kapsar |
|:--- |:--- |
| **AD FS yönetme** | |
| [Onarım hello güven](#repairthetrust) |Nasıl toorepair hello Federasyon ile Office 365 güven. |
| [Alternatif oturum açma Kimliğini kullanarak Azure AD ile birleştirmek](#alternateid) | Alternatif oturum açma Kimliğini kullanarak Federasyon yapılandırma  |
| [Bir AD FS sunucu ekleme](#addadfsserver) |Nasıl tooexpand bir AD FS ile ek bir AD FS sunucu grubu. |
| [Bir AD FS Web uygulaması Ara Sunucusu Ekle](#addwapserver) |Nasıl tooexpand bir AD FS ile ek bir Web uygulaması Ara sunucusu (WAP) sunucu grubu. |
| [Bir Federasyon etki alanına ekleme](#addfeddomain) |Nasıl tooadd federe bir etki alanı. |
| [Merhaba SSL sertifikasını güncelleştir](active-directory-aadconnectfed-ssl-update.md)| Nasıl tooupdate hello SSL sertifikası için bir AD FS grubu. |
| **AD FS özelleştirme** | |
| [Özel şirket logosu veya çizim ekleme](#customlogo) |Nasıl toocustomize bir AD FS oturum açma sayfasında bir şirket logo ve çizim. |
| [Bir oturum açma açıklama ekleme](#addsignindescription) |Nasıl bir oturum açma tooadd sayfa açıklaması. |
| [AD FS talep kuralları değiştirme](#modclaims) |Nasıl toomodify AD FS için çeşitli Federasyon senaryoları talepleri. |

## <a name="manage-ad-fs"></a>AD FS yönetme
Hello Azure AD Connect Sihirbazı'nı kullanarak Azure AD CONNECT'te minimum kullanıcı katılımıyla çeşitli AD FS ile ilgili görevleri gerçekleştirebilirsiniz. Çalışan Başlangıç Sihirbazı tarafından Azure AD Connect'i yüklemeye bitirdikten sonra hello Sihirbazı'nı çalıştırabilirsiniz yeniden tooperform ek görevleri.

## Onarım hello güven<a name=repairthetrust></a>
Azure AD Connect toocheck hello geçerli durumunu hello AD FS ve Azure AD güveni kullanın ve uygun eylemleri toorepair hello güven gerçekleştirin. Bu adımları toorepair izleyin, Azure AD ve AD FS güven.

1. Seçin **onarım AAD ve ADFS güven** ek görevleri hello listesinden.
   ![Onarım AAD ve ADFS güveni](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)

2. Merhaba üzerinde **tooAzure AD Connect** sayfasında, Azure AD genel yönetici kimlik bilgilerinizi sağlayın ve tıklayın **sonraki**.
   ![TooAzure AD connect](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)

3. Merhaba üzerinde **uzaktan erişim kimlik bilgileri** sayfasında, hello etki alanı yöneticisi hello kimlik bilgilerini girin.

   ![Uzaktan erişim kimlik bilgileri](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    Tıklattıktan sonra **sonraki**, Azure AD Connect için sertifika durumu denetler ve sorunları gösterir.

    ![Sertifika durumu](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    Merhaba **hazır tooconfigure** sayfa gösterir hello olacaktır eylemlerin listesini gerçekleştirilen toorepair hello güven.

    ![Hazır tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. Tıklatın **yükleme** toorepair hello güven.

> [!NOTE]
> Azure AD Connect can yalnızca onarma veya otomatik olarak imzalanan sertifikalar vermemizi. Azure AD Connect, üçüncü taraf sertifikalarının onarılamıyor.

## AlternateID kullanarak Azure AD ile birleştirmek<a name=alternateid></a>
Bunu hello içi kullanıcı asıl Name(UPN) ve kullanıcı asıl adı tutulur hello Bulut aynı hello önerilir. Merhaba içi UPN (örn. yönlendirilemeyen bir etki alanı kullanıyorsa Contoso.local) ya da değiştirilemez toolocal uygulama bağımlılıkları öneririz alternatif oturum açma kimliği ayarlama Alternatif oturum açma kimliği, bir oturum açma deneyimi posta gibi kendi UPN dışında bir öznitelik oturum nerede kullanıcılar oturum tooconfigure sağlar. Azure AD Connect varsayılan toohello userPrincipalName özniteliğindeki Active Directory kullanıcı asıl adı için Hello seçimdir. Kullanıcı asıl adı için başka bir öznitelik seçin ve AD FS kullanarak federasyonunu, ardından Azure AD Connect alternatif oturum açma kimliği için AD FS yapılandırma Kullanıcı asıl adı için farklı bir öznitelik seçme örneği aşağıda verilmiştir:

![Alternatif kimlik öznitelik seçimi](media/active-directory-aadconnect-federation-management/attributeselection.png)

AD FS için alternatif oturum açma Kimliğini yapılandırma iki ana adımdan oluşur:
1. **Merhaba sağ verme talep kümesini yapılandırmak**: hello verme talep kurallarıyla hello Azure AD bağlı olan taraf güven alternatif hello kullanıcının Kimliğini hello gibi değiştirilmiş toouse seçili hello UserPrincipalName özniteliği olan.
2. **Alternatif oturum açma kimliği hello AD FS yapılandırması etkinleştirme**: hello AD FS yapılandırması, böylece kullanıcılar hello uygun ormanlarda hello alternatif kimliğini kullanarak AD FS arayabilir güncelleştirilir Bu yapılandırma, AD FS için Windows Server 2012 R2 (KB2919355) veya sonraki sürümlerde desteklenir. Merhaba AD FS 2012 R2 sunuculardır, Azure AD Connect hello hello varlığını denetler KB gereklidir. Merhaba KB algılanmazsa, yapılandırma tamamlandıktan sonra bir uyarı aşağıda gösterildiği gibi görüntülenir:

    ![KB 2012R2 üzerinde eksik uyarı](media/active-directory-aadconnect-federation-management/kbwarning.png)

    eksik KB durumunda toorectify hello yapılandırmasını yüklemek gerekli hello [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) ve güven hello kullanarak Onar [AAD onarın ve AD FS güven](#repairthetrust).

> [!NOTE]
> AlternateID ve adımları toomanually hakkında daha fazla bilgi için yapılandırma, okuma [alternatif oturum açma Kimliğini yapılandırma](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)

## Bir AD FS sunucu ekleme<a name=addadfsserver></a>

> [!NOTE]
> tooadd bir AD FS sunucusu, Azure AD Connect hello PFX sertifikası gerektirir. Bu nedenle, yalnızca hello AD FS grubunu Azure AD Connect kullanarak yapılandırdıysanız bu işlemi gerçekleştirebilir.

1. Seçin **ek bir Federasyon Sunucusu'nu Dağıtma**, tıklatıp **sonraki**.

   ![Ek Federasyon sunucusu](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. Merhaba üzerinde **tooAzure AD Connect** sayfasında, Azure AD genel yönetici kimlik bilgilerinizi girin ve tıklayın **sonraki**.

   ![TooAzure AD connect](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. Merhaba etki alanı yönetici kimlik bilgilerini sağlayın.

   ![Etki alanı yönetici kimlik bilgileri](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. Azure AD Connect Azure AD Connect ile yeni AD FS grubunuzu yapılandırılırken sağlanmış hello PFX dosyasının hello parola ister. Tıklatın **parolasını girin** hello PFX dosyası tooprovide hello parolası.

   ![Sertifika parolası](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![SSL sertifikasını belirtin](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. Merhaba üzerinde **AD FS sunucuları** hello sunucu adı veya IP adresi toobe eklenen want toohello AD FS grubu.

   ![AD FS sunucuları](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. Tıklatın **sonraki**ve hello son Git **yapılandırma** sayfası. Azure AD Connect hello sunucuları toohello AD FS grubu ekleme tamamlandıktan sonra hello seçeneği tooverify hello bağlantısı verilir.

   ![Hazır tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Yükleme tamamlandı](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## Bir AD FS WAP sunucusu ekleme<a name=addwapserver></a>

> [!NOTE]
> tooadd WAP sunucusu, Azure AD Connect hello PFX sertifikası gerektirir. Bu nedenle, Azure AD Connect kullanarak hello AD FS grubunu yapılandırdıysanız bu işlemi yalnızca gerçekleştirebilirsiniz.

1. Seçin **Web uygulaması proxy'si dağıtmak** hello kullanılabilir görevler listesinden.

   ![Web uygulaması Ara sunucusu](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. Hello Azure genel yönetici kimlik bilgilerini sağlayın.

   ![TooAzure AD connect](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. Merhaba üzerinde **belirtin SSL sertifikası** sayfasında, Azure AD Connect ile Merhaba AD FS grubu yapılandırıldığında, sağladığınız hello PFX dosyasının hello parola sağlayın.
   ![Sertifika parolası](media/active-directory-aadconnect-federation-management/WapServer3.PNG)

    ![SSL sertifikasını belirtin](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. WAP sunucusu olarak eklenen hello sunucu toobe ekleyin. Merhaba WAP sunucusu etki alanına katılmış toohello olabilir çünkü hello sihirbaz eklenen yönetici kimlik bilgileri toohello sunucusu için sorar.

   ![Yönetim sunucusu kimlik bilgileri](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. Merhaba üzerinde **Proxy güven kimlik bilgilerini** sayfasında, yönetici kimlik bilgileri tooconfigure hello proxy hello AD FS grubunda, hello birincil sunucu güven ve erişim sağlayın.

   ![Proxy güven kimlik bilgileri](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. Merhaba üzerinde **hazır tooconfigure** sayfasında, hello Sihirbazı gerçekleştirilecek eylemler hello listesini gösterir.

   ![Hazır tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. Tıklatın **yükleme** toofinish hello yapılandırma. Merhaba Yapılandırma tamamlandıktan sonra seçeneği tooverify hello hello Sihirbazı verir bağlantı toohello sunucuları hello. Tıklatın **doğrula** toocheck bağlantısı.

   ![Yükleme tamamlandı](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## Bir Federasyon etki alanına ekleme<a name=addfeddomain></a>

Azure AD Connect kullanarak Azure AD ile bir etki alanı toobe federe kolay tooadd olur. Azure AD Connect hello etki alanını Federasyon ekler ve hello talep kuralları toocorrectly yansıtmak hello veren Azure AD ile birleştirildiyse birden çok etki alanınız olduğunda değiştirir.

1. tooadd bir Federasyon etki alanını seçin hello görev **ek bir ekleme Azure AD etki alanı**.

   ![Ek Azure AD etki alanı](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. Hello sonraki sayfada hello Sihirbazı'nın, Azure AD için hello genel yönetici kimlik bilgilerini sağlayın.

   ![TooAzure AD connect](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. Merhaba üzerinde **uzaktan erişim kimlik bilgileri** sayfasında, hello etki alanı yönetici kimlik bilgilerini sağlayın.

   ![Uzaktan erişim kimlik bilgileri](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. Merhaba sonraki sayfada, Başlangıç Sihirbazı, şirket içi dizininizle Azure AD etki alanlarının bir listesini sağlar. Merhaba etki alanı hello listeden seçin.

   ![Azure AD etki alanı](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    Hello etki alanını seçtikten sonra Başlangıç Sihirbazı, sihirbaz hello başka eylemler hakkında uygun bilgilerle alın ve hello yapılandırma etkisini hello sağlar. Bazı durumlarda, Azure AD'de hello Sihirbazı ile bilgi toohelp sağlar henüz doğrulandı olmayan bir etki alanı seçerseniz hello etki alanını doğrulayın. Bkz: [özel etki alanı adı tooAzure Active Directory eklemek](../active-directory-add-domain.md) daha fazla ayrıntı için.

5. **İleri**’ye tıklayın. Merhaba **hazır tooconfigure** sayfası hello Azure AD Connect gerçekleştireceği eylemlerin listesini gösterir. Tıklatın **yükleme** toofinish hello yapılandırma.

   ![Hazır tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> Merhaba kullanıcılardan mümkün toologin tooAzure AD olabilmesi Federasyon etki alanını eşitlenmesi gereken eklendi.

## <a name="ad-fs-customization"></a>AD FS özelleştirmesi
Merhaba aşağıdaki bölümler hello yaygın görevlerden bazıları hakkında ayrıntılar AD FS oturum açma sayfanız özelleştirdiğinizde tooperform olabilir sağlar.

## Özel şirket logosu veya çizim ekleme<a name=customlogo></a>
Merhaba üzerinde görüntülenen hello şirketin toochange hello logosunu **oturum açma** sayfasında, aşağıdaki Windows PowerShell cmdlet'ini ve sözdizimini hello kullanın.

> [!NOTE]
> Merhaba Hello logosu için bir dosya boyutu 10 KB'den büyük olmaması 96 dpi'de 260 x 35 boyutları önerilir.

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> Merhaba *TargetName* parametresi gereklidir. AD FS ile yayımlanan hello varsayılan tema varsayılan olarak adlandırılır.

## Bir oturum açma açıklama ekleme<a name=addsignindescription></a>
bir oturum açma sayfası açıklaması toohello tooadd **oturum açma sayfası**, Windows PowerShell cmdlet'ini ve sözdizimini aşağıdaki hello kullanın.

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## AD FS talep kuralları değiştirme<a name=modclaims></a>
AD FS kullanabileceğiniz bir zengin talep dili destekler toocreate özel talep kuralları. Daha fazla bilgi için bkz: [hello talep kuralı dili rolü hello](https://technet.microsoft.com/library/dd807118.aspx).

Merhaba aşağıdaki bölümlerde tooAzure AD ve AD FS federasyon ile ilgili bazı senaryolar için özel kurallar nasıl yazabilirsiniz açıklanmaktadır.

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a>Merhaba özniteliğinde bulunmasına değere koşullu bir sabit kimlik
Azure AD Connect nesneleri olduğunda kaynak bağlantısı tooAzure AD eşitlenmiş olarak kullanılan bir özniteliği toobe belirtmenize olanak sağlar. Merhaba değer hello özel öznitelik boş değilse, tooissue bir değişmez kimliği talebi isteyebilirsiniz.

Örneğin, seçebilirsiniz **ms ds consistencyguid** hello kaynak bağlantısı ve sorunu hello özniteliği olarak **İmmutableıd** olarak **ms ds consistencyguid** içindeki case hello öznitelik karşısında bir değer içeriyor. Merhaba özniteliği karşı değer yoksa, sorunu **objectGUID** değişmez kimliği hello gibi Bölümden hello açıklandığı gibi hello özel talep kuralları kümesi oluşturabilirsiniz.

**Kural 1: Sorgu öznitelikleri**

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

Bu kuralda hello değerlerini sorgulama **ms ds consistencyguid** ve **objectGUID** Active Directory'den hello kullanıcı için. Merhaba deposu tooan uygun depolama adı, AD FS dağıtımında değiştirin. Ayrıca hello talep tooa uygun talep türü, Federasyon için tanımlanan değiştirme **objectGUID** ve **ms ds consistencyguid**.

Kullanarak Ayrıca, **ekleme** ve **sorunu**, hello varlık için giden sorun eklemekten kaçının ve başlangıç değerleri Ara değer olarak kullanabilirsiniz. Hangi değer toouse değişmez kimliği hello gibi kurduktan sonra bir sonraki kuralında hello talep verecek

**Kural 2: ms ds consistencyguid hello kullanıcısı için olup olmadığını kontrol edin.**

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

Bu kural adlı geçici bir bayrak tanımlar **idflag** ayarlanan çok**useguid** yoksa hiçbir **ms ds consistencyguid** hello kullanıcı için doldurulur. Bu arkasındaki Hello mantığı, AD FS boş talep izin vermeyen hello gerçeğidir. Kural 1'de talep http://contoso.com/ws/2016/02/identity/claims/objectguid ve http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid eklediğinizde, şunun için bir **msdsconsistencyguid** talep eksikse Merhaba değeri hello kullanıcı için doldurulur. Doldurulmuş değil, AD FS boş değere sahip olur ve hemen bırakır görür. Tüm nesneler sahip **objectGUID**, kural 1 yürütüldükten sonra bu talep böylece her zaman vardır olur.

**3. kural: varsa, ms ds consistencyguid değişmez kimliği olarak verme**

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

Örtülü budur **mevcut** denetleyin. Hello talep için başlangıç değeri varsa, daha sonra değişmez hello kimliği sorun Merhaba önceki örnek kullanır hello **NameIdentifier** talep. Ortamınızda hello değişmez kimliği için bu toohello uygun talep türü toochange gerekir.

**Kural 4: ms ds consistencyGuid mevcut değilse objectGUID değişmez kimliği olarak verme**

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

Bu kuralda, yalnızca hello geçici bayrağı denetimi **idflag**. Tooissue hello talep tabanlı olup olmadığını karar değerini üzerinde.

> [!NOTE]
> Bu kurallar Hello sırası önemlidir.

### <a name="sso-with-a-subdomain-upn"></a>Bir alt etki alanı UPN SSO'su
Azure AD Connect kullanarak açıklandığı gibi Federasyon birden fazla etki alanı toobe ekleyebilirsiniz [yeni bir Federasyon etki alanına eklemek](active-directory-aadconnect-federation-management.md#addfeddomain). Böylece Hello verenin kimliği toohello kök etki alanı ve değil hello alt etki alanı, karşılık gelen hello Federasyon kök etki alanı da hello alt kapsar çünkü hello kullanıcı asıl adı (UPN) talebi değiştirmeniz gerekir.

Varsayılan olarak, hello talep kuralı verenin Kimliğini olarak ayarlamak için:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Varsayılan veren kimliği talebi](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

Merhaba varsayılan kuralı yalnızca hello UPN sonekini alır ve hello veren kimliği talebi kullanır. Örneğin, John sub.contoso.com içinde bir kullanıcıdır ve contoso.com Azure AD ile birleştirildiyse. John girer john@sub.contoso.com tooAzure AD imzalarken kullanıcıadı hello gibi. Merhaba varsayılan veren kimliği talep kuralı AD FS'de, aşağıdaki şekilde hello işleme:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

**Talep değeri:** http://sub.contoso.com/adfs/services/trust/

toohave yalnızca hello kök etki alanında hello verenin talep değeri, hello talep kuralı toomatch hello şu değiştirin:

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [kullanıcı oturum açma seçenekleri](active-directory-aadconnect-user-signin.md).
