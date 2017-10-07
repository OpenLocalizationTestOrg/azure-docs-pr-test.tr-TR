---
title: "aaaAzure çok faktörlü kimlik doğrulaması ile ilgili SSS | Microsoft Docs"
description: "Sık sorulan sorular ve yanıtlar tooAzure çok faktörlü kimlik doğrulaması ile ilgili. Çok faktörlü kimlik doğrulaması birden çok kullanıcı adı ve parola gerektiren bir kullanıcının kimlik doğrulama yöntemidir. Güvenlik toouser oturum açma ve işlemleri ek katmanı sağlar."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8305cf4c41bf8e9802df192fecdb7e463eff9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-multi-factor-authentication"></a>Azure çok faktörlü kimlik doğrulaması hakkında sık sorulan sorular
Bu SSS, Azure multi-Factor Authentication ve hello çok faktörlü kimlik doğrulama hizmeti kullanma hakkında sık sorulan soruları yanıtlar. Bunu hello hizmeti hakkında sorular içine genel olarak, modelleri, kullanıcı deneyimleri, faturalama ve sorun giderme ayrılmıştır.

## <a name="general"></a>Genel
**S: Azure multi-Factor Authentication sunucusu kullanıcı verileri nasıl işler?**

Multi-Factor Authentication sunucusu ile kullanıcı verileri yalnızca hello şirket içi sunucularda depolanır. Kalıcı kullanıcı verileri hello bulutta depolanır. Merhaba kullanıcı iki aşamalı doğrulama gerçekleştirdiğinde, multi-Factor Authentication sunucusu veri toohello kimlik doğrulaması için Azure multi-Factor Authentication bulut hizmetine gönderir. Merhaba çok faktörlü kimlik doğrulaması bulut hizmeti ile çok faktörlü kimlik doğrulama sunucusu arasında iletişimi 443 giden bağlantı noktası üzerinden Güvenli Yuva Katmanı (SSL) veya Aktarım Katmanı Güvenliği (TLS) kullanır.

Kimlik doğrulama isteklerini toohello bulut hizmetine gönderildiğinde kimlik doğrulama ve kullanım verileri toplanır raporlar. İki aşamalı doğrulama günlüklerinde dahil veri alanları aşağıdaki gibidir:

* **Benzersiz kimliği** (ya da kullanıcı adı veya şirket içi çok faktörlü kimlik doğrulama sunucusu kimliği)
* **İlk ve son adı** (isteğe bağlı)
* **E-posta adresi** (isteğe bağlı)
* **Telefon numarası** (sesli arama veya SMS kimlik doğrulaması kullanırken)
* **Cihaz belirteci** (mobil uygulama kimlik doğrulaması kullanırken)
* **Kimlik doğrulama modu**
* **Kimlik doğrulaması sonucu**
* **Çok faktörlü kimlik doğrulama sunucu adı**
* **Çok faktörlü kimlik doğrulama sunucusu IP**
* **İstemci IP** (varsa)

Merhaba isteğe bağlı alanları multi-Factor Authentication Sunucusu'nda yapılandırılabilir.

Doğrulama sonucu (başarılı veya engelleme) hello ve reddedildiyse, hello neden hello kimlik doğrulama verileriyle depolanır. Bu veriler, kimlik doğrulama ve kullanım raporlarında kullanılabilir.

## <a name="billing"></a>Faturalandırma
Çoğu faturalama soruları tooeither hello başvurarak yanıtlanması [çok faktörlü kimlik doğrulaması Fiyatlandırma sayfasında](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) veya hello belgelerine [nasıl tooget Azure çok faktörlü kimlik doğrulaması](multi-factor-authentication-versions-plans.md).

**S: hello telefon aramaları yapmak ve kimlik doğrulaması için kullanılan metin iletileri göndermek için sizden ücret Kuruluşum mi?**

Hayır, tek tek yerleştirilen aramaları için sizden ücret istenmese veya metin iletileri toousers Azure çok faktörlü kimlik doğrulaması üzerinden gönderilebilir. Bir kimlik doğrulaması başına MFA sağlayıcısı kullanırsanız, her kimlik doğrulama için ancak değil kullanılan hello yöntemi için faturalandırılır.

Kullanıcılarınızın hello telefon aramaları veya aldıkları, metin iletileri according tootheir Kişisel Telefon hizmeti için sizden ücret.

**S: Merhaba kullanıcı başına faturalama modelini bana tüm etkin kullanıcıları veya yalnızca hello iki aşamalı doğrulamayı gerçekleştirilen olanlar için ücretli mi?**

Faturalama iki aşamalı doğrulamayı o ay gerçekleştirilip bağımsız olarak yapılandırılmış kullanıcılar toouse çok faktörlü kimlik doğrulaması, hello sayısını temel alır.

**S: çok faktörlü kimlik doğrulaması faturalama nasıl çalışır?**

Kullanıcı başına veya kimlik doğrulaması başına MFA sağlayıcısı oluşturduğunuzda, kuruluşunuzun Azure aboneliği aylık kullanıma dayalı faturalandırılır. Bu fatura modelini benzer toohow Azure bills sanal makinelerin ve Web sitelerinde kullanım için.

Azure çok faktörlü kimlik doğrulaması için bir abonelik satın aldığınızda, kuruluşunuzun her kullanıcı için yalnızca hello yıllık lisans ücreti ödenen. MFA lisansları ve Office 365, Azure AD Premium veya Enterprise Mobility + güvenlik paketleri bu şekilde faturalandırılır. 

Seçenekleriniz hakkında daha fazla bilgi [nasıl tooget Azure çok faktörlü kimlik doğrulaması](multi-factor-authentication-versions-plans.md).

**S: Azure multi-Factor Authentication ücretsiz sürümü var mı?**

Bazı durumlarda, Evet.

Azure yöneticileri için çok faktörlü kimlik doğrulama erişim için herhangi bir ücret ödemeden Azure MFA özelliklerinin bir kısmı hello Azure ve Office 365 Yönetici portalı dahil olmak üzere tooMicrosoft çevrimiçi hizmetleri sunar. Bu teklif yalnızca tooglobal Yöneticiler hello MFA lisans, bir paket veya tek başına tüketim tabanlı sağlayıcı aracılığıyla Azure mfa tam sürüme sahip değilseniz Azure Active Directory örnekleri için geçerlidir. Yöneticilerinizin hello ücretsiz sürümünü kullanıyorsanız ve Azure MFA tam sürümünü satın alma, tüm genel yöneticileri sürümü otomatik olarak ücretli yükseltilmiş toohello olur.

Office 365 kullanıcıları için multi-Factor Authentication erişim için herhangi bir ücret ödemeden Azure MFA özelliklerinin bir kısmı Exchange Online ve SharePoint Online gibi tooOffice 365 hizmetleri sunar. Bu teklif, Azure Active Directory karşılık gelen örneği hello hello MFA lisans, bir paket veya tek başına tüketim tabanlı sağlayıcı aracılığıyla Azure mfa tam sürümüne sahip değil, atanan bir Office 365 lisansına sahip toousers geçerlidir.

**S: Kuruluşum, kullanıcı başına ve kimlik doğrulaması başına tüketim faturalama modelleri arasında herhangi bir zamanda geçiş yapabilirim?**

Tüketim tabanlı faturalama ile tek başına bir hizmet olarak MFA, kuruluşunuzun satın aldıysa, MFA sağlayıcısı oluşturduğunuzda faturalama modelini seçin. MFA sağlayıcısı oluşturulduktan sonra hello faturalama modeli değiştiremezsiniz. Ancak, hello MFA sağlayıcısı silin ve farklı bir fatura model biriyle oluşturun.

MFA sağlayıcısı oluşturulduğunda, bağlantılı tooan Azure Active Directory (diğer adıyla "Azure AD kiracısı") olabilir. Merhaba geçerli MFA sağlayıcısı bağlantılı tooan Azure AD Kiracı ise, güvenli bir şekilde hello MFA sağlayıcısını silmek ve bağlantılı toohello aynı Azure AD kiracısı olan bir oluşturun. Alternatif olarak, MFA için etkinleştirilen tüm kullanıcılar yeterli MFA, Azure AD Premium veya Enterprise Mobility + güvenlik (EMS) lisansı toocover satın aldıysanız, hello MFA sağlayıcısı tamamen silebilirsiniz.

MFA sağlayıcınızı ise *değil* bağlantılı tooan Azure AD Kiracı veya bağlantı hello yeni MFA sağlayıcısı tooa farklı Azure AD Kiracı, kullanıcı ayarlarını ve yapılandırma seçenekleri aktarılan değil. Ayrıca, Azure MFA sunucuları varolan aracılığıyla oluşturulan etkinleştirme kimlik bilgilerini kullanarak yeniden toobe yeni MFA sağlayıcısı hello. Merhaba MFA sunucuları toolink yeniden etkinleştirme bunları toohello yeni MFA sağlayıcısı telefon araması ve kısa mesaj kimlik doğrulamasını, ancak mobil uygulama bildirimleri hello mobil uygulama etkinleştirme kadar tüm kullanıcılar için çalışma durduracak etkilemez.

MFA sağlayıcıları hakkında daha fazla bilgi [Azure multi-Factor Auth sağlayıcısını kullanmaya başlama](multi-factor-authentication-get-started-auth-provider.md).

**S: Kuruluşum, herhangi bir zamanda tüketim tabanlı faturalama ve abonelik (lisans tabanlı modeli) arasında geçiş yapabilirim?**

Bazı durumlarda, Evet.

Dizininizde varsa bir *kullanıcı başına* Azure çok faktörlü kimlik doğrulama sağlayıcısı olarak MFA lisanslar ekleyebilirsiniz. Lisansına sahip olan kullanıcılar olmayan sayılır hello kullanıcı başına tüketim tabanlı faturalama içinde. Lisanssız kullanıcılar hello MFA sağlayıcısı üzerinden hala MFA için etkinleştirilebilir. Satın alma ve atarsanız, tüm kullanıcılar için lisans toouse çok faktörlü kimlik doğrulaması yapılandırılmış, hello Azure çok faktörlü kimlik doğrulama sağlayıcısı silebilirsiniz. Merhaba gelecekte daha fazla kullanıcı lisansı sayısından varsa, her zaman başka bir kullanıcı başına MFA sağlayıcısını oluşturabilirsiniz.

Dizininizde varsa bir *kimlik doğrulaması başına* Azure çok faktörlü kimlik doğrulama sağlayıcısı olarak her zaman bağlı tooyour abonelik hello MFA sağlayıcısı olduğu sürece her kimlik doğrulama için faturalandırılır. MFA lisansları toousers atayabilir, ancak bunu birinden bir MFA lisansı veya atanmış gelmediğini, hala her iki aşamalı doğrulama isteği için faturalandırılırsınız.

**S: mu Kuruluşum toouse var ve kimlikler toouse Azure multi-Factor Authentication eşitleme?**

Kuruluşunuz tüketim tabanlı faturalama modeli kullanıyorsa, Azure Active Directory isteğe bağlıdır, ancak gerekli değildir. MFA sağlayıcınızı bağlantılı tooan Azure AD kiracısı değilse, yalnızca Azure multi-Factor Authentication sunucusu veya hello Azure multi-Factor Authentication SDK'sı şirket içi dağıtabilirsiniz.

Lisans satın alın ve hello dizinindeki toousers Ata toohello Azure AD kiracısı eklendiğinden azure Active Directory hello lisans modeli için gereklidir.

## <a name="manage-and-support-user-accounts"></a>Yönetmek ve kullanıcı hesaplarını destekler

**S: ne my kullanıcılar toodo bunlar telefonlarını yanıtta almadığınız veya onlarla telefon yok söylemeliyim?**

Neyse tüm kullanıcılarınız birden fazla doğrulama yöntemi yapılandırılmış. Tekrar oturum açmayı tootry söyleyin ancak hello oturum açma sayfasında farklı bir doğrulama yöntemi seçin.

Kullanıcıların toohello gösterebilir [son kullanıcı sorun giderme kılavuzu](./end-user/multi-factor-authentication-end-user-troubleshoot.md).


**S: Kullanıcılarım birini tootheir hesabında alamazsa ne yapmalıyım?**

Merhaba kayıt işlemiyle toogo yeniden getirerek hello kullanıcının hesabı sıfırlayabilirsiniz. Daha fazla bilgi edinmek [hello bulutta Azure multi Factor Authentication ile kullanıcı ve cihaz ayarlarını yönetme](multi-factor-authentication-manage-users-and-devices.md).

**S: Kullanıcılarım birini uygulama parolaları kullanarak bir telefon kaybederse ne yapmalıyım?**

tooprevent yetkisiz erişim, tüm hello kullanıcının uygulama parolalarını Sil. Merhaba kullanıcı değiştirme aygıtın sonra hello parolaları yeniden oluşturabilirsiniz. Daha fazla bilgi edinmek [hello bulutta Azure multi Factor Authentication ile kullanıcı ve cihaz ayarlarını yönetme](multi-factor-authentication-manage-users-and-devices.md).

**S: Peki bir kullanıcı toonon tarayıcı uygulamalarında oturum açamaz?**

Kuruluşunuz eski istemcileri ve hala kullanıyorsa [uygulama parolaları hello kullanımına izin](multi-factor-authentication-whats-next.md#app-passwords), sonra da kullanıcılarınızın toothese eski istemcileri kullanıcı adı ve parola ile oturum açamazsınız. Bunun yerine, çok ihtiyaç duydukları[uygulama parolaları ayarlamanız](./end-user/multi-factor-authentication-end-user-app-passwords.md). Kullanıcılarınızın (silme) temizlemeniz gerekir, oturum açma bilgilerini hello uygulamayı yeniden başlatın ve kendi kullanıcı adıyla oturum ve *uygulama parolası* normal parolalarını yerine.

Kuruluşunuz eski istemciler yoksa, toocreate uygulama parolaları, kullanıcılarınızın izin.

> [!NOTE]
> Office 2013 istemcilerin için modern kimlik doğrulaması
>
> Uygulama parolaları yalnızca modern kimlik doğrulaması desteklemeyen uygulamalar için gereklidir. Office 2013 istemcileri modern kimlik doğrulama protokollerini destekler, ancak yapılandırılmış toobe gerekir. Yeni Office istemcileri otomatik olarak modern kimlik doğrulama protokollerini destekler. Daha fazla bilgi için bkz: Merhaba [Office 2013 modern kimlik doğrulaması genel önizlemesi duyuru](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

**S: kullanıcılar bazen hello metin iletisi almadığınız veya tootwo yönlü metin iletileri yanıtlayın ancak hello doğrulama zaman aşımına uğruyor söyleyin.**

Metin iletileri teslimini ve iki yönlü SMS yanıtlar alınmasını garanti edilmez hello hizmet hello güvenilirliğini etkileyebilecek denetlenemeyen Etkenler olduğundan. Bu etkenler hello hedef ülke, hello cep telefonu taşıyıcı ve hello sinyal gücü içerir.

Kullanıcılarınızın sık güvenilir bir şekilde metin iletileri alma sorunları varsa, bunun yerine toouse hello mobil uygulama veya telefon görüşmesi yöntemi söyleyin. Merhaba mobil uygulama hem cep ve Wi-Fi bağlantıları üzerinden bildirimleri alabilirsiniz. Ayrıca, hello Aygıt sinyali yok hiç olsa bile hello mobil uygulama doğrulama kodları oluşturabilirsiniz. Merhaba Microsoft Authenticator uygulaması için kullanılabilir [Android](http://go.microsoft.com/fwlink/?Linkid=825072), [IOS](http://go.microsoft.com/fwlink/?Linkid=825073), ve [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071).

Metin iletileri kullanmanız gerekiyorsa, iki yönlü SMS mümkün olduğunda yerine tek yönlü SMS kullanmanızı öneririz. Tek yönlü SMS daha güvenilirdir ve kullanıcıların başka bir ülkeden gönderildiği yanıtlama tooa metin iletisi genel SMS ücretleri doğurmasını engeller.

**S: Merhaba süreyi hello sistem zaman aşımına uğramadan önce Kullanıcılarım tooenter hello doğrulama kodunu metin iletisi sahip değiştirmek?**

Bazı durumlarda, Evet. 

Tek yönlü SMS için Azure MFA sunucusu v7.0 veya daha yüksek bir kayıt defteri anahtarı ayarını hello zaman aşımı yapılandırabilirsiniz. Merhaba MFA bulut hizmeti hello kısa mesaj gönderir sonra hello doğrulama kodu (veya bir kerelik geçiş kodu) toohello MFA sunucusu döndürülür. Merhaba MFA sunucusu varsayılan olarak 300 saniye bellekte hello kodunu depolar. Merhaba kullanıcı hello kod hello önce girmezse 300 saniye geçtiğinde, kendi kimlik doğrulaması reddedildi. Ayarı bu adımları toochange hello varsayılan zaman aşımı kullanın:

1. TooHKLM\Software\Wow6432Node\Positive Networks\PhoneFactor gidin.
2. Adlı bir DWORD kayıt defteri anahtarı oluşturun **pfsvc_pendingSmsTimeoutSeconds** ve hello Azure MFA sunucusu toostore bir kerelik geçiş kodlarını istediğiniz saniye cinsinden başlangıç saati ayarlayın.

>[!TIP] 
>Birden çok MFA sunucusu varsa, yalnızca hello hello özgün kimlik doğrulama isteği işleyen bir toohello kullanıcı gönderildiği hello doğrulama kodu bilir. Merhaba kullanıcı hello kodu girdiğinde, bu gönderileceği toohello kimlik doğrulama isteği toovalidate hello aynı sunucu. Merhaba kod doğrulama tooa farklı sunucu gönderilirse hello kimlik doğrulaması reddedildi. 

Azure MFA sunucusu ile iki yönlü SMS hello MFA Yönetim Portalı hello zaman aşımı ayarını yapılandırabilirsiniz. Kullanıcıların toohello SMS hello tanımlı zaman aşımı süresi içinde yanıt vermezseniz kendi kimlik doğrulaması reddedildi. 

(Merhaba AD FS bağdaştırıcısı ya da hello ağ ilkesi sunucusu uzantısı dahil) hello bulutta Azure MFA ile tek yönlü SMS hello zaman aşımı ayarını yapılandıramazsınız. Azure AD 180 saniye hello doğrulama kodunu depolar. 

**S: Azure multi-Factor Authentication sunucusu ile donanım belirteçleri kullanın?**

Azure multi-Factor Authentication sunucusu kullanıyorsanız, üçüncü taraf açık kimlik doğrulama (OATH) zamana dayalı, bir kerelik parola (TOTP) belirteçleri almak ve bunları iki aşamalı doğrulama için kullanın.

Bir CSV dosyasında hello gizli anahtar yerleştirin ve tooAzure çok faktörlü kimlik doğrulama sunucusu alın, OATH TOTP belirteçleri ActiveIdentity belirteçler kullanabilirsiniz. Merhaba istemci sistemi hello kullanıcı girişi kabul edebilir sürece OATH belirteçleri Active Directory Federasyon Hizmetleri (ADFS), Internet Information Server (IIS) Form tabanlı kimlik doğrulama ve Uzaktan Kimlik Doğrulama Çevirmeli Kullanıcı Hizmeti (RADIUS) kullanabilirsiniz.

Üçüncü taraf OATH TOTP belirteçleri biçimleri aşağıdaki hello ile aktarabilirsiniz:  

- Taşınabilir simetrik anahtar kapsayıcısı (PSKC)  
- Bir seri numarası, gizli bir anahtar temel 32 biçiminde ve bir zaman aralığı Hello dosya içeriyorsa, CSV  

**S: Azure multi-Factor Authentication sunucusu toosecure Terminal Hizmetleri kullanan?**

Windows Server 2012 R2 kullanıyorsanız veya daha sonra yalnızca Terminal Hizmetleri Uzak Masaüstü Ağ Geçidi (RD Ağ Geçidi) kullanarak güvenliğini sağlayabilirsiniz ancak Evet.

Windows Server 2012 R2'deki güvenlik değişiklikleri, Azure multi-Factor Authentication sunucusu toohello yerel güvenlik yetkilisi (LSA) güvenlik paketi, Windows Server 2012 ve önceki sürümlerinde nasıl bağlandığını değiştirildi. Terminal Hizmetleri Windows Server 2012 veya önceki sürümleri için şunları yapabilirsiniz [uygulama Windows kimlik doğrulaması ile güvenli](multi-factor-authentication-get-started-server-windows.md#to-secure-an-application-with-windows-authentication-use-the-following-procedure). Windows Server 2012 R2 kullanıyorsanız, RD Ağ Geçidi gerekir.

**S: arayan kimliği MFA sunucusunda yapılandırılmış, ancak kullanıcılar multi-Factor Authentication aramalarını anonim bir çağrıyı yapandan almaya devam.**

Bazen multi-Factor Authentication aramalarını hello ortak telefon ağ üzerinden yerleştirildiğinde, bunlar arayan kimliği desteği olmayan bir taşıyıcı yönlendirilir Merhaba çok faktörlü kimlik doğrulama sistemi her zaman, gönderdiği olsa bile bu nedenle, arayan kimliği, garanti edilmez.

**S: neden Kullanıcılarım istendiğinde tooregister kendi güvenlik bilgileri yükleniyor?**
Kullanıcıların verebilir birkaç nedeni vardır, güvenlik bilgilerini istendiğinde tooregister olabilir:

- Merhaba kullanıcı MFA için yönetici tarafından Azure AD'de etkinleştirildi, ancak kendi hesabı için henüz kayıtlı güvenlik bilgileri yok.
- Merhaba kullanıcı Self Servis parola sıfırlama Azure AD'de etkinleştirildi. Merhaba güvenlik bilgileri bunları bunlar herhangi bir zamanda unutursanız hello gelecekteki içinde kullanarak parolalarını sıfırlayabilir yardımcı olur.
- Merhaba kullanıcı bir koşullu erişim ilkesi toorequire MFA ve MFA için önceden kayıtlı olmayan bir uygulama erişilir.
- Merhaba kullanıcı (Azure AD katılım dahil), Azure AD ile bir cihaz kaydetme ve kuruluşunuzun cihaz kaydı için MFA gerekir, ancak hello kullanıcı daha önce MFA'ya kayıtlı değil.
- Merhaba kullanıcı (MFA gerektiren) Windows 10 iş için Windows Hello oluşturuyor ve MFA için daha önce kaydedilen kurmadı.
- Merhaba kuruluş, oluşturulan ve uygulanan toohello kullanıcı MFA kaydından ilkesi etkinleştirilmiş.
- Merhaba kullanıcı daha önce MFA'ya kayıtlı ancak yönetici beri devre dışı olan bir doğrulama yöntemi seçin. Merhaba kullanıcı MFA kaydından bu nedenle gitmek gerekir yeniden tooselect yeni bir varsayılan doğrulama yöntemi.


## <a name="errors"></a>Hatalar
**S: Bunlar mobil uygulamasının bildirimleri kullanırken, "kimlik doğrulama isteği etkinleştirilmiş bir hesap için değil" hata iletisi görürseniz kullanıcılar ne?**

Toofollow söyleyin bu yordamı tooremove hesaplarında hello mobil uygulamadan ekleyin yeniden:

1. Çok Git[Azure portal profilinizi](https://account.activedirectory.windowsazure.com/profile/) ve kuruluş hesabınızla oturum açın.
2. Seçin **ek güvenlik doğrulaması**.
3. Merhaba mobil uygulamadan Hello mevcut hesabı kaldırın.
4. Tıklatın **yapılandırma**ve ardından hello yönergeleri tooreconfigure hello mobil uygulama izleyin.

**S: Bunlar tooa tarayıcı olmayan uygulamada oturum açarken 0x800434D4L hata iletisi görürseniz kullanıcılar ne?**

iki aşamalı doğrulama gerektiren bir hesap ile çalışmayan bir yerel bilgisayarda yüklü tooa tarayıcı olmayan uygulamada toosign çalıştığınızda hello 0x800434D4L hata oluşur.

Bu hata için geçici çözüm toohave ayrı kullanıcı hesapları için yönetici ile ilgili olan ve olmayan yönetici işlemleri. Daha sonra böylece tooOutlook yönetici olmayan hesabınızı kullanarak oturum yönetici hesabı ve yönetici olmayan hesapta arasında posta kutularını bağlayabilirsiniz. Bu çözüm hakkında daha fazla ayrıntı için nasıl çok öğrenin[bir kullanıcının posta özelliği tooopen ve görünüm Merhaba içeriğine bir yönetici hello vermek](http://help.outlook.com/141/gg709759.aspx?sl=1).

## <a name="next-steps"></a>Sonraki adımlar
Lütfen sorunuzu burada cevaplanıp değil, hello sayfanın hello sonundaki hello açıklamalarında bırakın. Ya da Yardım almak için bazı ek seçenekleri şunlardır:

* Arama hello [Microsoft destek bilgi bankasına](https://www.microsoft.com/en-us/Search/result.aspx?form=mssupport&q=phonefactor&form=mssupport) çözümleri toocommon teknik sorunlar için.
* Arama ve teknik sorular ve yanıtlar hello topluluktan göz atın veya kendi hello soru [Azure Active Directory forumları](https://social.msdn.microsoft.com/Forums/azure/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).
* Eski PhoneFactor müşteri iseniz ve sorularınız varsa ya da parola sıfırlama yardıma gereksinim hello kullan [parola sıfırlama](mailto:phonefactorsupport@microsoft.com) tooopen bir destek servis talebi bağlantı.
* Aracılığıyla destek uzmanına başvurun [Azure çok faktörlü kimlik doğrulama sunucusu (PhoneFactor) Destek](https://support.microsoft.com/oas/default.aspx?prid=14947). Sorununuzu mümkün olduğunca hakkında kadar bilgi dahil ederseniz bize kurulurken yardımcı olur. Sağladığınız bilgileri nerede hello hata, hello özel hata kodu, hello belirli bir oturum kimliği ve hello hello hata gördüğünüz hello kullanıcının Kimliğini gördüğünüzü hello sayfa içerir.
