---
title: "Azure multi-Factor Authentication ve Active Directory arasında aaaDirectory tümleştirme"
description: "Bu nasıl toointegrate hello Azure çok faktörlü kimlik doğrulama sunucusu Active Directory ile Merhaba dizinleri eşitleyebilmeniz açıklayan hello Azure multi-Factor authentication sayfasıdır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: def7a534-cfb2-492a-9124-87fb1148ab1f
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fbff518b4641010d5f7745096e0ff658864d0805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="directory-integration-between-azure-mfa-server-and-active-directory"></a>Azure MFA Sunucusu ile Active Directory arasında dizin tümleştirme
Active Directory veya başka bir LDAP dizini ile hello Azure MFA sunucusu toointegrate Hello dizin tümleştirme bölümü kullanın. Öznitelikleri toomatch hello directory şeması yapılandırabilir ve otomatik kullanıcı eşitlemeyi ayarlama.

## <a name="settings"></a>Ayarlar
Varsayılan olarak, hello Azure çok faktörlü kimlik doğrulama (MFA) sunucusu yapılandırılmış tooimport ya da Active Directory'den kullanıcıları eşitlemeye.  Merhaba dizin tümleştirme sekmesi, toooverride hello varsayılan davranış ve toobind tooa farklı bir LDAP dizini, ADAM dizini ya da belirli Active Directory etki alanı denetleyicisi sağlar.  Ayrıca LDAP kimlik doğrulaması tooproxy LDAP hello kullanımını veya LDAP bağı olarak RADIUS hedefi, IIS kimlik doğrulaması veya kullanıcı portalı için birincil kimlik doğrulaması için ön kimlik doğrulamasını sağlar.  Aşağıdaki tablonun hello hello tek tek ayarlar açıklanır.

![Ayarlar](./media/multi-factor-authentication-get-started-server-dirint/dirint.png)

| Özellik | Açıklama |
| --- | --- |
| Active Directory Kullan |Hello kullan Active Directory seçeneği toouse Active Directory içeri aktarma ve eşitleme için seçin.  Merhaba varsayılan ayar budur. <br>Not: İçin Active Directory Tümleştirme toowork düzgün katılın hello bilgisayar tooa etki alanı ve bir etki alanı hesabı ile oturum açın. |
| Güvenilen etki alanlarını dahil et |Denetleme **güvenilen etki alanlarını dahil et** tarafından güvenilen geçerli etki alanı, başka bir hello ormandaki etki alanı veya orman güvenine dahil etki alanları hello toohave hello Aracısı girişimi tooconnect toodomains.  İçeri aktarma veya hello hiçbirini kullanıcılardan eşitleme güvenilen etki alanları, hello onay kutusunu tooimprove performans seçeneğinin işaretini kaldırın.  Merhaba varsayılan olarak işaretlidir. |
| Özel LDAP yapılandırması kullan |İçeri aktarma ve eşitleme için belirtilen hello LDAP kullan seçeneğini toouse hello LDAP ayarları seçin. Not: LDAP Kullan seçildiğinde, hello kullanıcı arabirimi, başvuruları Active Directory tooLDAP değiştirir. |
| Düzenle düğmesi |Merhaba Düzenle düğmesi hello geçerli LDAP yapılandırması ayarları toomodified sağlar. |
| Öznitelik kapsam sorgularını kullan |Öznitelik kapsam sorgularının kullanılıp kullanılmaması gerektiğini gösterir.  Öznitelik kapsam sorgularını başka bir kaydın özniteliğindeki hello girdileri temel alarak kayıtları nitelendiren etkili dizin aramalarına izin verir.  Hello Azure çok faktörlü kimlik doğrulama sunucusu bir güvenlik grubunun bir üyesi olan öznitelik kapsam sorguları tooefficiently sorgusu hello kullanıcıları kullanır.   <br>Not: Öznitelik kapsam sorgularının desteklendiği bazı durumlar vardır, ancak kullanılmamalıdır.  Örneğin, Active Directory bir güvenlik grubu birden fazla etki alanı üyesini içerdiğinde, öznitelik kapsam sorgularıyla sorun yaşayabilir. Bu durumda, hello onay kutusunun seçimini kaldırın. |

Aşağıdaki tablonun hello hello LDAP yapılandırma ayarları açıklanmaktadır.

| Özellik | Açıklama |
| --- | --- |
| Sunucu |Merhaba ana bilgisayar veya hello LDAP dizinini çalıştıran hello sunucusunun IP adresini girin.  Noktalı virgülle ayrılarak bir yedek sunucu de belirtilebilir. <br>Not: Bağlama Türü SSL olduğunda, tam bir ana bilgisayar adı gerekir. |
| Temel DN	 |Merhaba, tüm dizin sorgularının Başlat hello temel dizin nesnesinin ayırt edici adını girin.  Örneğin, dc=abc,dc=com. |
| Bağlama türü - Sorgular |Toosearch hello LDAP dizinine bağlanırken kullanmak için Hello uygun bağ türünü seçin.  Bu, içeri aktarımlar, eşitleme ve kullanıcı adı çözümleme için kullanılır. <br><br>  Anonim - Anonim bir bağlama gerçekleştirilir.  Bağlama DN’si ve Bağlama Parolası kullanılmaz.  Bu, yalnızca hello LDAP dizini anonim bağlamaya izin verirse ve izinler hello hello uygun kayıtların ve özniteliklerin sorgulanmasına izin verirseniz çalışır.  <br><br> Basit - bağlama DN'si ve bağlama parolası düz metin toobind toohello LDAP dizini olarak geçirilir.  Bu test amacıyla, sunucu hello tooverify ulaştı ve bu hello bağ hesabının hello uygun erişime sahip. Merhaba uygun sertifika yüklendikten sonra bunun yerine SSL kullanın.  <br><br> SSL - bağlama DN'si ve bağlama parolası, SSL toobind toohello LDAP dizini kullanılarak şifrelenir.  LDAP dizini güvenleri hello bir sertifikanın yerel olarak yükleyin.  <br><br> Windows - bağlama kullanıcı adı ve bağ parolası olan kullanılan toosecurely bağlanmak tooan Active Directory etki alanı denetleyicisine veya ADAM dizinine.  Bağ kullanıcı adı boş bırakılırsa hello oturum açmış kullanıcının kullanılan toobind hesabıdır. |
| Bağlama türü - Kimlik doğrulamaları |LDAP bağlama kimlik doğrulaması gerçekleştirirken kullanmak için Hello uygun bağlama türünü seçin.  Merhaba Bağ türü açıklamalarını Bağ türü - sorgular altında bakın.  Örneğin, bu SSL bağlama kullanılan toosecure LDAP bağı kimlik doğrulamalarını olsa da sorgular için kullanılan anonim bağlama toobe için sağlar. |
| Bağlama DN’si veya Bağlama kullanıcı adı |Merhaba ayırt edici adını hello kullanıcı kaydına hello hesap toouse için toohello LDAP dizinine bağlanırken girin.<br><br>Merhaba bağ ayırt edici adı yalnızca bağlama türü basit ya da SSL olduğunda kullanılır.  <br><br>Bağ türü Windows olduğunda toohello LDAP dizinine bağlanırken hello Windows hesabı toouse Hello kullanıcı adı girin.  Boş bırakılırsa, hello oturum açmış kullanıcının kullanılan toobind hesabıdır. |
| Bağlama Parolası |Merhaba hello bağ DN için bağ parolasını ya da kullanılan toobind toohello LDAP dizini olan kullanıcı adı girin.  Merhaba multi-Factor Auth sunucusu AdSync hizmeti, tooconfigure hello parola eşitlemeyi etkinleştir ve hello hizmet hello yerel makinede çalıştığından emin olun.  Merhaba parola, multi-Factor Auth sunucusu AdSync Hizmeti'nin çalıştığı hello hesap hello altında hello Windows'ta depolanan kullanıcı adları ve parolalar bölümüne kaydedilir.  Merhaba parola da multi-Factor Auth sunucusu kullanıcı arabirimi olarak ve hello hesap hello multi-Factor Auth sunucusu Hizmeti'nin altında çalıştığı çalıştığı hello hesap hello altında kaydedilir.  <br><br>Merhaba parola yalnızca hello yerel sunucunun Windows kayıtlı kullanıcı adları ve parolalar kaydedildiği, erişim toohello parola gereken her multi-Factor Auth sunucusu bu adımı yineleyin. |
| Sorgu boyutu sınırı |Merhaba hello en fazla dizin araması döndürür kullanıcı sayısı için boyut sınırını belirtin.  Bu sınır hello LDAP dizini hello yapılandırma ile eşleşmesi gerekir.  Burada disk belleği desteklenmiyor büyük arar içeri aktarma ve eşitleme tooretrieve kullanıcıları toplu halde çalışır.  Merhaba boyut sınırı burada hello LDAP dizininde yapılandırılan hello sınırından daha büyük belirtilirse, bazı kullanıcılar eksik olabilir. |
| Test düğmesi |Tıklatın **Test** tootest bağlama toohello LDAP sunucusu.  <br><br>Tooselect hello gerekmeyen **LDAP kullan** seçeneği tootest bağlama. Bu hello LDAP yapılandırması kullanmadan önce test hello bağlama toobe sağlar. |

## <a name="filters"></a>Filtreler
Filtreleri tooset ölçütleri tooqualify kayıtları, dizin araması yaparken sağlar.  Ayarı hello Filtresi tarafından kapsamını belirleyebilirsiniz hello nesneleri toosynchronize istiyor.  

![Filtreler](./media/multi-factor-authentication-get-started-server-dirint/dirint2.png)

Azure çok faktörlü kimlik doğrulaması üç filtre seçenekleri aşağıdaki hello sahiptir:

* **Kapsayıcı filtresi** -dizin araması yaparken kullanılan tooqualify kapsayıcı kayıtlarını hello filtre ölçütlerini belirtin.  Active Directory ve ADAM için yaygın olarak (|(objectClass=organizationalUnit)(objectClass=container)) kullanılır.  Diğer LDAP dizinleri için her hello dizin şemasına bağlı olarak, kapsayıcı nesnesinin türünü niteleyen filtre ölçütü kullanın.  <br>Not: Boş bırakılırsa varsayılan olarak ((objectClass=organizationalUnit)(objectClass=container)) kullanılır.
* **Güvenlik grubu filtresini** -dizin araması yaparken kullanılan tooqualify güvenlik grubu kayıtlarını hello filtre ölçütlerini belirtin.  Active Directory ve ADAM için yaygın olarak (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)) kullanılır.  Diğer LDAP dizinleri için her hello dizin şemasına bağlı olarak güvenlik grubu nesnesinin türünü niteleyen filtre ölçütü kullanın.  <br>Not: Boş bırakılırsa varsayılan olarak (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)) kullanılır.
* **Kullanıcı filtresi** -dizin araması yaparken kullanılan tooqualify kullanıcı kayıtlarını hello filtre ölçütlerini belirtin.  Active Directory ve ADAM için yaygın olarak (&(objectClass=user)(objectCategory=person)) kullanılır.  Diğer LDAP dizinleri için kullanın (objectClass = inetOrgPerson) veya benzeri, hello dizin şemasına bağlı olarak. <br>Not: Boş bırakılırsa varsayılan olarak (&(objectCategory=person)(objectClass=user)) kullanılır.

## <a name="attributes"></a>Öznitelikler
Belirli bir dizinin özniteliklerini gerektiği şekilde özelleştirebilirsiniz.  Bu tooadd özel öznitelikler verir ve ihtiyacınız hello eşitleme tooonly hello öznitelikleri ince ayar. Her öznitelik alanı hello değerini hello dizin şemasında tanımlandığı şekilde hello attricute Hello adını kullanın. Merhaba aşağıdaki tabloda her bir özellik hakkında ek bilgi sağlar.

Öznitelikler el ile girilebilir ve gerekli toomatch hello öznitelik listesindeki bir öznitelikle değildir.

![Öznitelikler](./media/multi-factor-authentication-get-started-server-dirint/dirint3.png)

| Özellik | Açıklama |
| --- | --- |
| Benzersiz tanımlayıcı |Merhaba hello kapsayıcı, güvenlik grubu ve kullanıcı kayıtlarının benzersiz tanımlayıcısı hizmet hello özniteliğin öznitelik adını girin.  Active Directory'de, bu genellikle objectGUID’dir. Diğer LDAP uygulamaları entryUUID veya benzerini kullanabilir.  Merhaba, objectGUID varsayılandır. |
| Benzersiz tanımlayıcı türü |Merhaba hello benzersiz tanımlayıcı özniteliği türünü seçin.  Active Directory'de hello objectGUID özniteliği GUID tipidir. Diğer LDAP uygulamaları ASCII Bayt Dizisi ya da Dize türü kullanabilir.  Merhaba, GUID varsayılandır. <br><br>Bu tür doğru eşitleme öğeleri bu yana kendi benzersiz tanımlayıcısı tarafından başvurulan önemli tooset olur. Merhaba benzersiz tanımlayıcı türü kullanılan toodirectly Bul hello hello dizininde nesnesidir.  Bu tür tooString Hello dizin, hello değeri gerçekte ASCII karakterlerin bayt dizisi olarak depolar. zaman ayarlamak eşitlemenin düzgün çalışmasını engeller. |
| Ayırt edici ad |Merhaba her kayıt için hello ayırt edici adını içeren hello özniteliğin öznitelik adını girin.  Active Directory'de, bu genellikle distinguishedName’dir. Diğer LDAP uygulamaları entryDN veya benzerini kullanabilir.  Merhaba, distinguishedName varsayılandır. <br><br>Yalnızca hello ayırt edici adı içeren bir öznitelik yoksa, hello adspath özniteliği kullanılabilir.  Merhaba "LDAP: / /\<server\>/" Merhaba yol bölümü otomatik olarak çıkarılmış kapalı, yalnızca hello nesnesinin ayırt edici adını hello bırakarak. |
| Kapsayıcı adı |Merhaba hello bir kapsayıcı kaydındaki adı içeren hello özniteliğin öznitelik adını girin.  Bu özniteliğin Hello değeri, hello kapsayıcı hiyerarşisi görüntülenir, Active Directory'den içe aktarırken veya eşitleme öğeleri eklerken.  Merhaba varsayılan addır. <br><br>Farklı kapsayıcılar kendi adları için farklı öznitelikler kullanıyorsa, birden çok kapsayıcı adı özniteliği noktalı tooseparate kullanın.  Merhaba ilk kapsayıcı adı özniteliği bir kapsayıcı nesnesinde bulunan kullanılan toodisplay adıdır. |
| Güvenlik grubu adı |Merhaba hello bir güvenlik grubu kaydındaki adı içeren hello özniteliğin öznitelik adını girin.  Bu özniteliğin Hello değeri, hello güvenlik grubu listesinde görüntülenir, Active Directory'den içe aktarırken veya eşitleme öğeleri eklerken.  Merhaba varsayılan addır. |
| Kullanıcı adı |Merhaba hello kullanıcı bir kullanıcı kaydındaki adı içeren hello özniteliğin öznitelik adını girin.  Bu özniteliğin değeri Hello hello multi-Factor Auth sunucusu kullanıcı adı olarak kullanılır.  İkinci bir öznitelik önce yedekleme toohello belirtilebilir.  Merhaba ilk öznitelik hello kullanıcı için bir değer içermemesi halinde hello ikinci öznitelik sadece kullanılır.  Merhaba varsayılanlar userPrincipalName ve sAMAccountName ' dir. |
| Ad |Merhaba hello bir kullanıcı kaydındaki adı içeren hello özniteliğin öznitelik adını girin.  Merhaba, givenName varsayılandır. |
| Soyadı |Merhaba hello Soyadı bir kullanıcı kaydındaki içeren hello özniteliğin öznitelik adını girin.  Merhaba, sn varsayılandır. |
| E-posta adresi |Merhaba hello e-posta adresi bir kullanıcı kaydındaki içeren hello özniteliğin öznitelik adını girin.  E-posta adresidir kullanılan toosend Hoş Geldiniz ve güncelleştirme e-postaları toohello kullanıcı.  Merhaba, mail varsayılandır. |
| Kullanıcı grubu |Merhaba hello bir kullanıcı kaydındaki kullanıcı grubunu içeren hello özniteliğin öznitelik adını girin.  Kullanıcı grubu kullanılan toofilter kullanıcıları hello aracısı ve hello multi-Factor Auth sunucusu Yönetim Portalı raporlarında olabilir. |
| Açıklama |Merhaba hello tanımı bir kullanıcı kaydındaki içeren hello özniteliğin öznitelik adını girin.  Açıklama yalnızca arama için kullanılır.  Merhaba, description varsayılandır. |
| Telefon araması dili |Merhaba hello kısa adını hello dil toouse yönelik sesli aramalar hello kullanıcı için içeren hello özniteliğin öznitelik adını girin. |
| SMS dili |Merhaba hello kısa adını hello dil toouse yönelik SMS iletileri hello kullanıcı için içeren hello özniteliğin öznitelik adını girin. |
| Mobil uygulama dili |Merhaba hello kısa adını hello dil toouse hello kullanıcı için telefon uygulama metin iletileri için içeren hello özniteliğin öznitelik adını girin. |
| OATH belirteci dili |Merhaba hello kısa adını hello dil toouse hello kullanıcı OATH belirteci SMS mesajlarında içeren hello özniteliğin öznitelik adını girin. |
| İş telefonu |Merhaba hello bir kullanıcı kaydındaki iş telefonu numarasını içeren hello özniteliğin öznitelik adını girin.  Merhaba, telephoneNumber varsayılandır. |
| Ev telefonu |Merhaba hello bir kullanıcı kaydındaki ev telefonu numarasını içeren hello özniteliğin öznitelik adını girin.  Merhaba, homePhone varsayılandır. |
| Çağrı cihazı |Merhaba hello bir kullanıcı kaydındaki çağrı cihazı numarasını içeren hello özniteliğin öznitelik adını girin.  Merhaba, pager varsayılandır. |
| Cep telefonu |Merhaba hello bir kullanıcı kaydındaki cep telefonu numarasını içeren hello özniteliğin öznitelik adını girin.  Merhaba varsayılan olarak mobile'dir. |
| Faks |Merhaba hello bir kullanıcı kaydındaki faks numarasını içeren hello özniteliğin öznitelik adını girin.  Merhaba, facsimileTelephoneNumber varsayılandır. |
| IP telefonu |Merhaba hello bir kullanıcı kaydındaki IP telefonu numarasını içeren hello özniteliğin öznitelik adını girin.  Merhaba, ipPhone varsayılandır. |
| Özel |Merhaba bir kullanıcı kaydındaki özel telefonu numarasını içeren hello özniteliğin öznitelik adını girin.  Merhaba varsayılan boştur. |
| Dahili numara |Merhaba hello telefon numarası dahili bir kullanıcı kaydındaki içeren hello özniteliğin öznitelik adını girin.  Merhaba uzantı alanı Hello değeri hello uzantısı toohello sadece birincil telefon numarasının kullanılır.  Merhaba varsayılan boştur. <br><br>Merhaba uzantısı özniteliği belirtilmezse, uzantıları hello telefon özniteliğinin bir parçası olarak dahil olabilir. Bu durumda, böylece doğru Ayrıştırılan bir 'x' hello uzantısıyla koyun.  Örneğin, 555-123-4567 x890 hello telefon numarası olarak 555-123-4567 ve hello uzantısı olarak 890 ile sonuçlandı. |
| Varsayılanları Geri Yükle düğmesi |Tıklatın **Varsayılanları Geri Yükle** tooreturn tootheir varsayılan değer tüm öznitelikler yedekleyin.  Merhaba Varsayılanları hello normal Active Directory veya ADAM şeması ile düzgün çalışması gerekir. |

tooedit öznitelikleri tıklatın **Düzenle** hello öznitelikler sekmesinde.  Bu, hello öznitelikleri düzenleyebileceğiniz bir pencereyi getirir. Select hello **...**  sonraki tooany özniteliği tooopen hangi özniteliklerin toodisplay seçebileceğiniz bir pencere.

![Öznitelikleri Düzenleme](./media/multi-factor-authentication-get-started-server-dirint/dirint4.png)

## <a name="synchronization"></a>Eşitleme
Eşitleme hello Azure MFA kullanıcı veritabanını Active Directory veya başka bir Basit Dizin Erişim Protokolü (LDAP) dizin hello kullanıcılarla eşitlenmiş tutar. Merhaba işlem benzer tooimporting kullanıcıları Active Directory'den el ile ancak Active Directory kullanıcısı için düzenli aralıklarla yoklar ve güvenlik grubu tooprocess değiştirir.  Ayrıca, bir kapsayıcıdan, güvenlik grubundan ya da Active Directory’den kaldırılan kullanıcıları devre dışı bırakır veya kaldırır.

Merhaba multi-Factor Auth ADSync hizmeti, Active Directory yoklaması düzenli hello gerçekleştiren bir Windows hizmetidir.  Bu Azure AD eşitleme veya Azure AD Connect ile kafası toobe değildir.  Merhaba multi-Factor Auth ADSync, aynı kod tabanıyla oluşturulmakla birlikte belirli toohello Azure çok faktörlü kimlik doğrulama sunucusu olur.  Durdurulmuş durumda yüklenir ve hello yapılandırıldığında multi-Factor Auth Sunucusu hizmeti tarafından başlatılan toorun.  Çok sunuculu multi-Factor Auth sunucusu yapılandırmanız varsa, hello multi-Factor Auth ADSync yalnızca tek bir sunucu üzerinde çalışabilir.

Merhaba multi-Factor Auth ADSync hizmeti hello değişiklikleri Microsoft tooefficiently yoklama tarafından sağlanan DirSync LDAP sunucu uzantısını kullanır.  Bu DirSync kontrol arayanı hello "directory get değişiklikleri" sağ ve DS-Replication-Get-Changes genişletilmiş Denetim erişim hakkı olmalıdır.  Varsayılan olarak, bu haklar etki alanı denetleyicilerinde toohello yönetici ve LocalSystem hesaplarına atanır.  Merhaba multi-Factor Auth AdSync hizmeti varsayılan olarak LocalSystem olarak yapılandırılmış toorun şeklindedir.  Bu nedenle, en basit toorun hello bir etki alanı denetleyicisinde hizmetidir.  Yapılandırırsanız, hello hizmet tooalways tam eşitleme gerçekleştirmek, daha az izne sahip bir hesap gibi çalışabilir.  Bu daha az verimlidir, ancak daha az hesap ayrıcalığı gerektirir.

Merhaba LDAP dizini destekler ve ise DirSync için yapılandırıldıktan sonra yoklama kullanıcı ve güvenlik grubu değişikliklerinin çalışabilmesi için hello aynı Active Directory ile yaptığı gibi.  Sonra Hello LDAP dizini hello DirSync denetimini desteklemiyorsa, her döngü sırasında tam eşitleme gerçekleştirilir.

![Eşitleme](./media/multi-factor-authentication-get-started-server-dirint/dirint5.png)

Merhaba aşağıdaki tabloda hello eşitleme sekmesini ayarların her biri hakkında daha fazla bilgi içerir.

| Özellik | Açıklama |
| --- | --- |
| Active Directory ile eşitlemeyi etkinleştir |İşaretlendiğinde, hello multi-Factor Auth Sunucusu hizmeti Active Directory değişikliklerini düzenli aralıklarla yoklar. <br><br>Not: en az bir eşitleme öğesi eklenmeli ve Şimdi Eşitle hello multi-Factor Auth Sunucusu hizmeti değişiklikleri işlemeye başlamadan önce gerçekleştirilmesi gerekir. |
| Şu aralıkta eşitle |Merhaba zaman aralığı hello multi-Factor Auth sunucusu hizmetinin değişiklikleri yoklama ve işleme arasında bekleyeceği belirtin. <br><br> Not: Belirtilen hello hello her döngünün başlangıcı arasındaki hello zaman aralığıdır.  Merhaba süresi işleme değişiklikleri hello aralığı aşarsa, hello hizmet hemen tekrar yoklama yapar. |
| Artık Active Directory'de olmayan kullanıcıları kaldır |İşaretlendiğinde, hello multi-Factor Auth Sunucusu hizmeti Active Directory silinmiş kullanıcı işaretlerini işler ve Kaldır hello ilgili multi-Factor Auth sunucusu kullanıcı. |
| Her zaman tam eşitleme gerçekleştir |İşaretlendiğinde, hello multi-Factor Auth Sunucusu hizmeti her zaman tam eşitleme gerçekleştirir.  İşaretlenmediğinde, hello multi-Factor Auth Sunucusu hizmeti yalnızca değiştirilmiş kullanıcılar sorgulayarak Artımlı eşitleme gerçekleştirir.  Merhaba varsayılan olarak işaretli değildir. <br><br>İşaretlenmediğinde, Azure MFA sunucusu yalnızca hello dizin hello DirSync denetimini destekliyorsa ve izinleri tooperform DirSync artımlı sorguları hello hesap bağlama toohello dizin sahip olduğunda Artımlı eşitleme gerçekleştirir.  Merhaba hesabı hello uygun izinlere sahip değil veya birden çok etki alanı hello eşitlemeye dahil, Azure MFA sunucusu tam eşitleme gerçekleştirir. |
| X değerinden fazla kullanıcı devre dışı bırakıldığında ya da kaldırıldığında yönetici onayı iste |Eşitleme öğeleri yapılandırılmış toodisable olması veya artık hello öğesi'nin kapsayıcı veya güvenlik grubunun bir üyesi olan kullanıcılar kaldırın.  Kullanıcıların toodisable veya Kaldır Hello sayısı eşiği aştığında koruyucu olarak yönetici onayı gerekli olabilir.  İşaretlenirse belirtilen eşik için onay gerekir.  Merhaba varsayılan 5'tir ve 1 too999 hello aralıktır. <br><br> Onay ilk bir e-posta bildirim tooadministrators gönderilmesiyle sağlanır. Merhaba e-posta bildirimi hello devre dışı bırakma ve kullanıcıların kaldırılmasını incelenmesi ve onaylanmasına ilişkin talimatlar sunar.  Merhaba multi-Factor Auth sunucusu kullanıcı arabirimi başlatıldığında, onay isteminde bulunur. |

Merhaba **Şimdi Eşitle** düğmesi sağlar, toorun tam eşitleme hello eşitleme için belirtilen öğeleri.  Eşitleme öğeleri eklendiğinde, değiştirildiğinde, kaldırıldığında ve yeniden sıralandığında her seferde tam eşitleme gereklidir.  Ayrıca, başlangıç noktası hello hizmet ondan artımlı değişiklikler için yoklama hello belirlediğinden önce gerekli hello multi-Factor Auth AdSync hizmeti çalışır durumda olduğunu.  Toosynchronization öğeleri yapılan değişiklikler, ancak tam eşitleme gerçekleştirilen taşınmadığından, istendiğinde tooSynchronize şimdi olacaktır.

Merhaba **kaldırmak** düğmesi hello multi-Factor Auth sunucusu Eşitleme öğesi listesinden bir veya daha fazla eşitleme öğeleri hello yönetici toodelete sağlar.

> [!WARNING]
> Eşitleme öğesi kaydı kaldırıldıktan sonra kurtarılamaz. Yanlışlıkla sildiyseniz, tooadd hello Eşitleme öğesi kaydı yeniden gerekir.

Merhaba Eşitleme öğesi veya eşitleme öğeleri multi-Factor Auth Sunucusu'ndan kaldırıldı.  Merhaba multi-Factor Auth Sunucusu hizmeti artık hello eşitleme öğelerini işlemeyecek.

Hello Yukarı Taşı ve Aşağı Taşı düğmeleri Merhaba yönetici toochange hello hello eşitleme öğelerinin sıralamasını sağlar.  Merhaba aynı kullanıcı (örneğin bir kapsayıcı ve güvenlik grubu) birden fazla eşitleme öğesinin üyesi olabileceğinden hello sırası önemlidir.  Eşitleme sırasında uygulanan toohello kullanıcı hello ilk eşitleme öğesinden hello listesi toowhich hello kullanıcı gelecektir hello ayarları ilişkili değil.  Bu nedenle, hello eşitleme öğeleri öncelik sırasına sokulmalıdır.

> [!TIP]
> Eşitleme öğeleri kaldırıldıktan sonra bir tam eşitleme gerçekleştirilmelidir.  Eşitleme öğeleri sıralandıktan sonra bir tam eşitleme gerçekleştirilmelidir.  Tıklatın **Şimdi Eşitle** tooperform tam eşitleme.

## <a name="multi-factor-auth-servers"></a>Multi-Factor Auth Sunucuları
Ek multi-Factor Auth sunucuları tooserve yedek RADIUS proxy, LDAP proxy olarak ya da IIS kimlik doğrulaması için ayarlanmış olabilir. Merhaba eşitleme yapılandırması tüm hello aracılar arasında paylaşılır. Bununla birlikte, bu aracıları yalnızca biri çalışan hello multi-Factor Auth Sunucusu hizmeti olabilir. Bu sekme tooselect hello eşitleme için etkinleştirilmesi gereken multi-Factor Auth sunucusu sağlar.

![Multi-Factor Auth Sunucuları](./media/multi-factor-authentication-get-started-server-dirint/dirint6.png)
