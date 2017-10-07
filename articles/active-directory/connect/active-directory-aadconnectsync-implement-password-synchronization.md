---
title: "Azure AD Connect eşitleme ile aaaImplement parola eşitleme | Microsoft Docs"
description: "Parola Eşitleme nasıl çalışır ve nasıl hakkında bilgi sağlar tooset ayarlama."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 05f16c3e-9d23-45dc-afca-3d0fa9dbf501
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: a0401640f2a4d914419ee4446f923bb3a972389d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a>Azure AD Connect eşitleme ile parola eşitlemeyi uygulama
Bu makalede örneğinden şirket içi Active Directory örneği tooa bulut tabanlı Azure Active Directory (Azure AD) kullanıcı parolalarınızı toosynchronize gereken bilgileri sağlar.

## <a name="what-is-password-synchronization"></a>Parola Eşitleme nedir
Merhaba olasılık tooa Unutulan parolayı işinizi alma engellenen ilgili toohello numarası farklı parolalarını tooremember gerekir. Daha fazla parolaları tooremember, hello yüksek hello olasılık tooforget bir gereksinim hello. Sorular ve parola sıfırlama ve diğer parola ile ilgili sorunları talep hakkında çağrıları çoğu Yardım Masası kaynakları hello.

Parola eşitleme özelliği toosynchronize kullanıcı parolalarını şirket içi Active Directory örneğini Azure AD bulut tabanlı tooa örneğinden kullanılır.
Bu özellik toosign tooAzure AD Hizmetleri Office 365, Microsoft Intune, CRM Online ve Azure Active Directory etki alanı Hizmetleri (Azure AD DS) gibi kullanın. Toohello hizmetinde oturum hello kullanarak aynı parola kullandığınız toosign tooyour içinde Active Directory örneğine şirket.

![Azure AD Connect nedir?](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

Parola Hello sayısını azaltarak, kullanıcılarınızın toomaintain toojust biri gerekir. Parola Eşitleme, yardımcı olur:

* Merhaba, kullanıcılarınızın verimliliğini artırır.
* Yardım Masası maliyetlerini azaltır.  

Ayrıca, toouse karar verirseniz [Active Directory Federasyon Hizmetleri (AD FS) ile Federasyon](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect), AD FS altyapınızı başarısız olursa, isteğe bağlı olarak parola eşitleme yedek olarak ayarlayabilirsiniz.

Parola Eşitleme Azure AD Connect eşitleme tarafından uygulanan bir uzantı toohello dizin eşitleme özelliğidir. toouse parola eşitleme, ortamınızdaki şunları yapmanız gerekir:

* Azure AD Connect'i yükleme.  
* Şirket içi Active Directory örneğinizi ve Azure Active Directory örneğinizi arasında dizin eşitlemesi yapılandırın.
* Parola eşitlemeyi etkinleştir.

Daha ayrıntılı bilgi için bkz. [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).

> [!NOTE]
> Azure Active Directory etki alanı FIPS ve parola eşitleme için yapılandırılmış hizmetleri hakkında daha fazla ayrıntı için bu makalenin sonraki bölümlerinde "Parola Eşitleme ve FIPS" konusuna bakın.
>
>

## <a name="how-password-synchronization-works"></a>Parola Eşitleme nasıl çalışır
Hello Active Directory etki alanı hizmeti hello gerçek kullanıcı parolası bir karma değer gösterimini hello formda parolaların saklar. Bir karma değer tek yönlü matematiksel işlevi sonucudur (Merhaba *karma algoritması*). Tek yönlü işlevin toohello düz metin sürümünün bir parola yöntemi toorevert hello sonuç yok. Parola karma toosign tooyour şirket ağında kullanamazsınız.

Azure AD Connect eşitleme parolanızı, parola karma değerden ayıklar toosynchronize şirket içi Active Directory örneğiyle hello. Ek güvenlik işleme uygulanan silinmeden önce toohello parola karması toohello Azure Active Directory kimlik doğrulama hizmeti eşitlenir. Parolalar, kullanıcı başına temelinde ve kronolojik sıraya göre eşitlenir.

Merhaba gerçek veri akışını hello parola eşitleme işlemi, kullanıcı verilerinin DisplayName veya e-posta adresleri gibi benzer toohello eşitleme olur. Ancak, parolalar hello standart dizin eşitleme penceresinde diğer öznitelikler için daha sık eşitlenir. Merhaba parola eşitleme işlemi 2 dakikada bir çalışır. Bu işlem hello sıklığı değiştirilemiyor. Parola Eşitleme sırasında hello mevcut bulut parolayı üzerine yazar.

Merhaba ilk kez hello parola eşitleme özelliği etkinleştirmek, tüm kapsam kullanıcıların hello parolaların bir başlangıç eşitlemesi gerçekleştirir. Bir alt kümesini toosynchronize istediğiniz kullanıcı parolalarını açıkça tanımlayamazsınız.

Bir şirket içi parola değiştirdiğinizde, güncelleştirilen hello parola, genellikle birkaç dakika içinde eşitlenir.
Merhaba parola eşitleme özelliği başarısız eşitleme girişimleri otomatik olarak yeniden dener. Bir hata, bir parola denemesi toosynchronize sırasında bir hata meydana gelirse, Olay Görüntüleyicisi'nde günlüğe kaydedilir.

Parola Hello eşitleme şu anda açık olan hello kullanıcı üzerinde etkisi yoktur.
Geçerli bulut hizmeti oturumunuz tooa bulut hizmetinde oturum açılırken oluşan eşitlenmiş parola değişikliği hemen etkilenmez. Ancak, Hello bulut hizmeti, tooauthenticate yeniden gerektirdiğinde, yeni parolanızı tooprovide gerekir.

Bir kullanıcı, bunlar tootheir şirket ağında oturum açtınız bağımsız olarak bir ikinci zaman tooauthenticate tooAzure AD, kullanıcının şirket kimlik bilgilerini girmeniz gerekir. Merhaba kullanıcı oturum açmada (KMSI) onay kutusuna hello bana imzalı Koru seçerse bu deseni, ancak en aza indirgenebilir. Bu seçim, kısa bir süre için kimlik doğrulaması atlayan bir oturum tanımlama bilgisi ayarlar. KMSI davranışı etkin veya hello Azure AD Yöneticisi tarafından devre dışı.

> [!NOTE]
> Parola Eşitleme, yalnızca Active Directory'de hello nesne türü kullanıcı için desteklenir. Merhaba iNetOrgPerson nesne türü için desteklenmiyor.

### <a name="detailed-description-of-how-password-synchronization-works"></a>Parola Eşitleme nasıl çalışır ayrıntılı açıklama
Merhaba aşağıdaki ayrıntılı parola eşitleme, Active Directory ve Azure AD arasında nasıl çalıştığını açıklar.

![Ayrıntılı parola akışı](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. Her iki dakikada hello parola eşitleme Aracısı hello AD Connect sunucusu üzerinde bir DC hello standart aracılığıyla gelen depolanan parola karmalarını (Merhaba unicodePwd özniteliği) istekleri [MS-DRSR](https://msdn.microsoft.com/library/cc228086.aspx) kullanılan toosynchronize veri çoğaltma Protokolü DC'lerin arasında. Merhaba hizmet hesabı dizin değişikliklerini çoğaltma ve çoğaltma dizin değişiklikleri tüm AD (yüklemesinde varsayılan olarak) izinler tooobtain hello parola karmaları olması gerekir.
2. Göndermeden önce hello DC hello MD4 parola karması bir anahtarı kullanarak şifreler bir [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) karma hello RPC oturum anahtarı ve bir veri dizesi. Ardından hello sonuç toohello parola eşitleme Aracısı RPC üzerinden gönderir. Merhaba DC ayrıca hello salt toohello eşitleme Aracısı hello aracı mümkün toodecrypt hello Zarf olacak şekilde hello DC çoğaltma protokolü kullanarak geçirir.
3.  Merhaba parola eşitleme Aracısı hello şifrelenmiş Zarf sahip olduktan sonra onu kullanır [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) ve salt toogenerate bir anahtar toodecrypt alınan hello veri geri tooits özgün MD4 biçiminde hello. Herhangi bir noktada hello parola eşitleme Aracısı erişim toohello düz metin parolası sahip. Merhaba parola eşitleme aracının MD5 kesinlikle hello DC ile çoğaltma Protokolü uyumluluk için kullanılır ve yalnızca şirket içi hello DC hello parola eşitleme Aracısı arasındaki kullanılır.
4.  Bu dize dönüştürme geri sonra UTF-16 kodlamalı ikili içine hello parola eşitleme Aracısı hello 16 bayt ikili parola karması too64 bayt ilk dönüştürme hello karma tooa 32 baytlık onaltılık dize tarafından genişletir.
5.  10 bayt uzunluğu salt oluşan bir salt Hello parola eşitleme Aracısı ekler, toohello 64-bayt ikili toofurther hello özgün karma koruma.
6.  Merhaba parola eşitleme Aracısı sonra hello MD4 karma artı salt birleştirir ve hello girdi [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) işlevi. Merhaba, 1000 yineleme [HMAC SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) anahtarlı karma algoritma kullanılır. 
7.  Hello parola eşitleme Aracısı hello elde edilen 32 baytlık karma alır, hem hello salt art arda ekler ve SHA256 yineleme tooit (tarafından kullanılmak üzere Azure AD) sayısı hello ardından SSL üzerinden Azure AD Connect tooAzure AD hello dizeden iletir.</br> 
8.  Ne zaman bir kullanıcı toosign tooAzure AD içinde çalışır ve kendi parola, hello parola girdiğinde hello çalıştırılan aynı MD4 + salt + PBKDF2 + HMAC SHA256 işlemi. Merhaba elde edilen karma Azure AD'de depolanan hello karma eşleşirse, hello kullanıcı hello doğru parolayı geçtiğini ve doğrulanır. 

>[!Note] 
>Merhaba özgün MD4 karma iletilen tooAzure AD değil. Bunun yerine, hello hello özgün MD4 karma SHA256 karma iletilir. Sonuç olarak, Azure AD'de depolanan hello karması alınıyorsa, bir şirket içi pass--hash saldırısında kullanılamaz.

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a>Parola Eşitleme Azure Active Directory etki alanı Hizmetleri ile nasıl çalışır
Ayrıca hello parola eşitleme özelliği toosynchronize şirket içi parolalarınızı çok kullanabilirsiniz[Azure Active Directory etki alanı Hizmetleri](../../active-directory-domain-services/active-directory-ds-overview.md). Bu senaryoda, hello Azure Active Directory etki alanı Hizmetleri örneği hello bulut, kullanıcılarınızın şirket içi Active Directory örneğinizi kullanılabilir tüm hello yöntemleriyle kimliğini doğrular. Merhaba bu senaryonun benzer toousing hello Active Directory Geçiş Aracı (ADMT) bir şirket içi ortamda deneyimidir.

### <a name="security-considerations"></a>Güvenlikle ilgili dikkat edilmesi gerekenler
Parola eşitleme yaparken hello düz metin parolanızı değil gösterilen toohello parola eşitleme özelliği, tooAzure AD veya ilişkili hello hizmetlerini sürümüdür.

Kullanıcı kimlik doğrulaması Azure ad yerine hello kuruluşun kendi Active Directory örneğiyle gerçekleşir. Kuruluşunuzun bırakarak herhangi bir biçimde parola verileri şirket içi Merhaba, o hello Azure AD'de--depolanan SHA256 parola verileri hello düşünmek endişeniz varsa hello özgün MD4 karma--karmasını Active Directory'de depolanan daha önemli ölçüde daha güvenli. Ayrıca, bu SHA256 karma şifresi çözülemiyor olduğundan, bu olamaz toohello kuruluşunuzun Active Directory ortamına geri getirildi ve bir geçerli kullanıcının parolası pass--hash saldırısı olarak sunulan.





### <a name="password-policy-considerations"></a>Parola ilke konuları
Parola eşitlemeyi etkinleştirerek etkilenen parola ilkeleri iki tür vardır:

* Parola karmaşıklık İlkesi
* Parola süre sonu ilkesi

#### <a name="password-complexity-policy"></a>Parola karmaşıklık İlkesi  
Parola Eşitleme etkinleştirildiğinde, şirket içi Active Directory Örneğinizde hello parola karmaşıklık ilkeleri eşitlenen kullanıcılar için hello bulutta karmaşıklık ilkeleri geçersiz kılar. Tüm hello geçerli parolalar, şirket içi Active Directory örneği tooaccess Azure AD hizmetlerinde kullanabilirsiniz.

> [!NOTE]
> Doğrudan hello bulutta oluşturulan kullanıcılar için parola hala hello bulutta tanımlanan konu toopassword ilkelerdir.

#### <a name="password-expiration-policy"></a>Parola süre sonu ilkesi  
Bir kullanıcı, parola eşitleme hello kapsamında ise, hello bulut hesap parolası çok ayarlayın*süresi dolmayacak*.

Şirket içi ortamınızda süresi eşitlenmiş bir parola kullanarak tooyour bulut Hizmetleri'nde toosign devam edebilirsiniz. Bulut parolanızı güncelleştirilmiş hello başlattığınızda hello şirket içi ortamda hello Parola Değiştir.

#### <a name="account-expiration"></a>Hesabın süre sonu
Kuruluşunuzun kullanıcı hesabı yönetimi bir parçası olarak hello accountExpires özniteliği kullanıyorsa, bu öznitelik eşitlenmiş tooAzure AD olmadığını unutmayın. Sonuç olarak, parola eşitlemesi için yapılandırılmış bir ortamda süresi dolmuş bir Active Directory hesabı Azure AD'de etkin olmaya devam eder. Merhaba hesap süresi dolmuşsa, bir iş akışı eylemi hello kullanıcının Azure AD hesabının devre dışı bırakan bir PowerShell Betiği tetiklemesi gereken öneririz. Merhaba hesap açıldığında, buna karşılık, hello Azure AD örneğinde açık olmalıdır.

### <a name="overwrite-synchronized-passwords"></a>Eşitlenmiş parolalar üzerine yaz
Bir yönetici el ile Windows PowerShell kullanarak parolanızı sıfırlayabilirsiniz.

Bu durumda, hello yeni parola eşitlenmiş parolanızı geçersiz kılar ve uygulanan toohello yeni parola hello bulutta tanımlanan tüm parola ilkelerini olur.

Şirket içi parolanızı yeniden değiştirirseniz, hello yeni parola değil toohello bulut eşitlenir ve el ile güncelleştirilmiş hello parola geçersiz kılar.

bir parola Hello eşitlenmesi hello açık olan Azure kullanıcı üzerinde etkisi yoktur. Geçerli bulut hizmeti oturumunuz tooa bulut hizmetinde oturum açtığınız sırada gerçekleşen eşitlenmiş parola değişikliği hemen etkilenmez. KMSI bu fark hello süresini uzatır. Merhaba bulut hizmeti, tooauthenticate yeniden gerektirdiğinde, yeni parolanızı tooprovide gerekir.

### <a name="additional-advantages"></a>Ek avantajlar

- Genellikle, parola eşitleme, bir Federasyon Hizmeti daha basit tooimplement içindir. Herhangi bir ek sunucu gerektirmez ve yüksek oranda kullanılabilir Federasyon Hizmeti tooauthenticate kullanıcıları bağımlılığı ortadan kaldırır. 
- Parola Eşitleme, toplama toofederation de etkinleştirilebilir. Federasyon hizmetinize bir kesinti oluşursa bir geri dönüş olarak kullanılabilir.












## <a name="enable-password-synchronization"></a>Parola eşitlemeyi etkinleştirme
Hello kullanarak Azure AD Connect yüklediğinizde **hızlı ayarlar** seçeneği, parola eşitleme otomatik olarak etkinleştirilir. Daha fazla ayrıntı için bkz: [hızlı ayarları kullanarak Azure AD Connect ile çalışmaya başlama](active-directory-aadconnect-get-started-express.md).

Azure AD Connect yüklediğinizde özel ayarları kullanırsanız, parola eşitleme hello kullanıcı oturum açma sayfasında kullanılabilir. Daha fazla ayrıntı için bkz: [Azure AD Connect özel yüklemesi](active-directory-aadconnect-get-started-custom.md).

![Parola Eşitleme etkinleştiriliyor](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a>Parola Eşitleme ve FIPS
Sunucunuz tooFederal bilgi işleme standardı (FIPS) according aşağı kilitlenmişse MD5 devre dışı bırakılır.

**Parola Eşitleme için MD5 tooenable hello aşağıdaki adımları gerçekleştirin:**

1. Too%ProgramFiles%\Azure AD Sync\Bin gidin.
2. Miiserver.exe.config açın.
3. Merhaba dosya hello sonunda toohello yapılandırma/çalışma zamanı düğümüne gidin.
4. Düğüm aşağıdaki hello ekleyin:`<enforceFIPSPolicy enabled="false"/>`
5. Yaptığınız değişiklikleri kaydedin.

Başvuru için bu kod parçacığında ne gibi görünmelidir şöyledir:

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

Güvenlik ve FIPS hakkında daha fazla bilgi için bkz: [AAD parola eşitleme, şifreleme ve FIPS Uyumluluk](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/).

## <a name="troubleshoot-password-synchronization"></a>Parola eşitleme sorunlarını giderme
Parola Eşitleme ile ilgili sorununuz olup [parola eşitleme sorunlarını giderme](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="next-steps"></a>Sonraki adımlar
* [Azure AD Connect eşitleme: eşitleme seçeneklerini özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
