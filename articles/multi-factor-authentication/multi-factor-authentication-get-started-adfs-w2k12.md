---
title: Windows Server AD FS'de sunucusuyla aaaMFA | Microsoft Docs
description: "Bu makalede, Azure multi-Factor Authentication ve AD FS Windows Server 2012 R2 ve 2016 tooget nasıl kullanmaya açıklanmaktadır."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/29/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 656785abcc63a020add765a86670b488a3b84b51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-in-windows-server"></a>Windows Server AD FS ile Azure multi-Factor Authentication sunucusu toowork yapılandırın
Active Directory Federasyon Hizmetleri (AD FS) kullanın ve toosecure Bulut veya şirket içi kaynakları istiyorsanız, AD FS ile Azure multi-Factor Authentication sunucusu toowork yapılandırabilirsiniz. Bu yapılandırma yüksek değerli uç noktalar için iki aşamalı doğrulamayı tetikler.

Bu makale Windows Server 2012 R2 veya Windows Server 2016’da AD FS ile Multi-Factor Authentication Sunucusu kullanmayı ele alır. Hakkında daha fazla bilgi için çok okuma[AD FS 2.0 ile Azure multi-Factor Authentication sunucusu kullanarak Bulut ve şirket içi kaynakları güvenli](multi-factor-authentication-get-started-adfs-adfs2.md).

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>Azure Multi-Factor Authentication Sunucusu ile Windows Server AD FS’yi güvenli hale getirme
Azure multi-Factor Authentication sunucusu yüklediğinizde aşağıdaki seçenekleri şu hello vardır:

* Azure multi-Factor Authentication Sunucusu'nu yerel olarak hello üzerinde yükleme olarak AD FS aynı sunucuya
* Hello Azure multi-Factor Authentication bağdaştırıcısı hello AD FS sunucu üzerinde yerel olarak yükleyin ve çok faktörlü kimlik doğrulama sunucusu farklı bir bilgisayarda yükleyin

Başlamadan önce aşağıdaki bilgilerle Merhaba dikkat edin:

* Gerekli tooinstall Azure multi-Factor Authentication sunucusu, AD FS sunucusunda değildir. Ancak, bir Windows Server 2012 R2 veya Windows Server 2016'de, AD FS çalıştıran AD FS için hello multi-Factor Authentication bağdaştırıcısı yüklemeniz gerekir. Desteklenen bir sürüm olduğu ve AD FS federasyon sunucunuzda hello AD FS bağdaştırıcısını ayrı olarak yüklerseniz, hello sunucusu başka bir bilgisayara yükleyebilirsiniz. Merhaba bkz yordamları toolearn nasıl tooinstall hello bağdaştırıcısı ayrı olarak.
* Kuruluşunuz metin iletisi ya da mobil uygulama doğrulama yöntemlerini kullanıyorsa, şirket Ayarları'nda tanımlanan hello dizelerini bir yer tutucu içeren <$*Uygulama_adı*$>. MFA Sunucusu v7.1’de bu yer tutucunun yerini alan bir uygulama adı belirtebilirsiniz. Merhaba AD FS bağdaştırıcısı kullandığınızda bu yer tutucu v7.0 veya daha eski, otomatik olarak değiştirilmez. Bu eski sürümleri için AD FS'yi güvenli hale getirdiğinizde hello yer tutucu hello uygun dizelerden kaldırılması.
* içinde toosign kullanmak hello hesabının kullanıcı hakları toocreate güvenlik grupları, Active Directory hizmetinde olmalıdır.
* Merhaba multi-Factor Authentication AD FS Bağdaştırıcısı Yükleme Sihirbazı Active Directory Örneğinizde PhoneFactor Admins adlı bir güvenlik grubu oluşturur. Ardından, başlangıç AD FS hizmet hesabı, Federasyon Hizmeti toothis grubunuzun ekler. Etki alanı denetleyicinizde PhoneFactor Admins grubunun gerçekten oluşturulduğunu bu hello ve hello AD FS hizmet hesabının bu grubun üyesi olduğunu doğrulayın. Gerekirse, el ile etki alanı denetleyicinizde hello AD FS hizmet hesabı toohello PhoneFactor Admins grubuna ekleyin.
* Merhaba Kullanıcı Portalı'yla hello Web hizmeti SDK'sını yükleme hakkında daha fazla bilgi için bilgiyi [Azure multi-Factor Authentication sunucusu için hello kullanıcı portalını dağıtma.](multi-factor-authentication-get-started-portal.md)

### <a name="install-azure-multi-factor-authentication-server-locally-on-hello-ad-fs-server"></a>Azure multi-Factor Authentication sunucusu hello AD FS sunucusunda yerel olarak yükle
1. Azure Multi-Factor Authentication Sunucusu’nu AD FS sunucunuza indirin ve yükleyin. Yükleme bilgileri için bkz. [Azure Multi-Factor Authentication Sunucusunu kullanmaya başlama](multi-factor-authentication-get-started-server.md).
2. Merhaba Hello Azure multi-Factor Authentication sunucusu yönetim konsolunda tıklatın **AD FS** simgesi. Merhaba seçeneklerini **kullanıcı kaydına izin ver** ve **tooselect yöntemi kullanıcıların**.
3. Kuruluşunuz için toospecify istediğiniz ek seçenekleri seçin.
4. **AD FS Bağdaştırıcısı’nı Yükle**'ye tıklayın.
   
   <center>![Bulut](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. Merhaba Active Directory penceresi görüntülenirse, iki şey anlamına gelir. Bilgisayarınızı birleştirilmiş tooa etki alanıdır ve hello AD FS bağdaştırıcısı ile Merhaba multi-Factor Authentication hizmeti arasındaki iletişimi korumak için hello Active Directory yapılandırması tamamlanmamışsa. Tıklatın **sonraki** tooautomatically bu yapılandırmayı tamamlamak ya da seçin hello **otomatik Active Directory yapılandırmasını atla ve ayarları yapılandırmak el ile** onay kutusu. **İleri**’ye tıklayın.
6. Yerel Grup windows Hello görüntülenir, iki şey anlamına gelir. Bilgisayarınızın etki alanına katılmış tooa değildir ve hello AD FS bağdaştırıcısı ile Merhaba multi-Factor Authentication hizmeti arasındaki iletişimi korumak için hello yerel Grup yapılandırması tamamlanmamışsa. Tıklatın **sonraki** tooautomatically bu yapılandırmayı tamamlamak ya da seçin hello **otomatik yerel grup yapılandırmasını atla ve ayarları yapılandırmak el ile** onay kutusu. **İleri**’ye tıklayın.
7. Merhaba Yükleme Sihirbazı'nda tıklatın **sonraki**. Azure multi-Factor Authentication sunucusu hello PhoneFactor Admins grubu oluşturur ve hello AD FS hizmet hesabı toohello PhoneFactor Admins grubuna ekler.
   <center>![Bulut](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. Merhaba üzerinde **yükleyiciyi Başlat** sayfasında, **sonraki**.
9. Merhaba multi-Factor Authentication AD FS bağdaştırıcısı yükleyicisinde tıklatın **sonraki**.
10. Tıklatın **Kapat** hello yükleme tamamlandığında.
11. Merhaba bağdaştırıcı yüklendiğinde AD FS ile kaydetmeniz gerekir. Windows PowerShell'i açın ve hello aşağıdaki komutu çalıştırın:<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![Bulut](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. toouse yeni kaydettiğiniz bağdaştırıcıyı, düzenleme hello genel kimlik doğrulama ilkesi AD FS'de. Merhaba AD FS yönetim konsolunda toohello Git **kimlik doğrulama ilkeleri** düğümü. Merhaba, **çok faktörlü kimlik doğrulaması** bölümünde, hello tıklatın **Düzenle** sonraki toohello bağlantı **genel ayarları** bölümü. Merhaba, **genel kimlik doğrulama ilkesini Düzenle** penceresinde, seçin **çok faktörlü kimlik doğrulaması** bir ek kimlik doğrulama yöntemi ve ardından olarak **Tamam**. Merhaba bağdaştırıcı WindowsAzureMultiFactorAuthentication olarak kaydedilir. Merhaba kayıt tootake etkisi Hello AD FS hizmetini yeniden başlatın.

<center>![Bulut](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

Bu noktada, çok faktörlü kimlik doğrulama sunucusu toobe bir ek kimlik doğrulama sağlayıcısı toouse AD FS ile ayarlanır.

## <a name="install-a-standalone-instance-of-hello-ad-fs-adapter-by-using-hello-web-service-sdk"></a>Hello Web hizmeti SDK'sını kullanarak hello AD FS bağdaştırıcısının tek başına örneğini yükleme
1. Merhaba Web hizmeti SDK multi-Factor Authentication sunucusu çalıştıran hello sunucuya yükleyin.
2. Kopya hello aşağıdaki dosyaları hello files\multi-Factor Authentication Server dizin toohello sunucusu tooinstall hello AD FS bağdaştırıcısı planladığınız:
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. Merhaba MultiFactorAuthenticationAdfsAdapterSetup64.msi yükleme dosyasını çalıştırın.
4. Merhaba multi-Factor Authentication AD FS bağdaştırıcısı yükleyicisinde tıklatın **sonraki** toostart hello yükleme.
5. Tıklatın **Kapat** hello yükleme tamamlandığında.

## <a name="edit-hello-multifactorauthenticationadfsadapterconfig-file"></a>Merhaba MultiFactorAuthenticationAdfsAdapter.config dosyasını düzenleyin
Bu adımları tooedit hello MultiFactorAuthenticationAdfsAdapter.config dosyasını izleyin:

1. Set hello **UseWebServiceSdk** düğümü çok**doğru**.  
2. Ayarlamak için hello değer **Webservicesdkurl'yi** hello çok faktörlü kimlik doğrulama Web hizmeti SDK'sı toohello URL'si. Örneğin: *https://contoso.com/&lt;certificatename&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*, burada *certificatename* sertifikanızı hello adıdır.  
3. Ekleyerek Hello Register-MultiFactorAuthenticationAdfsAdapter.ps1 betiğini düzenleyin *- ConfigurationFilePath &lt;yolu&gt;*  hello toohello sonuna `Register-AdfsAuthenticationProvider` komutu, burada  *&lt;yolu&gt;*  hello tam yolu toohello MultiFactorAuthenticationAdfsAdapter.config dosyasıdır.

### <a name="configure-hello-web-service-sdk-with-a-username-and-password"></a>Bir kullanıcı adı ve parola ile Merhaba Web hizmeti SDK'sını yapılandırın
Merhaba Web hizmeti SDK'sını yapılandırmak için iki seçenek vardır. Merhaba önce bir kullanıcı adı ve parola, hello ikinci bir istemci sertifikası ile. Merhaba ilk seçeneği için şu adımları izleyin veya İleri Merhaba ikinci atlayabilirsiniz.  

1. Ayarlamak için hello değer **WebServiceSdkUsername** hello PhoneFactor Admins güvenlik grubunun üyesi olan tooan hesap. Kullanım hello &lt;etki alanı&gt;&#92;&lt; Kullanıcı adı&gt; biçimi.  
2. Ayarlamak için hello değer **WebServiceSdkPassword** toohello uygun hesap parolası.

### <a name="configure-hello-web-service-sdk-with-a-client-certificate"></a>Bir istemci sertifikası ile Merhaba Web hizmeti SDK'sını yapılandırın
Bir kullanıcı adı ve parola toouse istemiyorsanız, bir istemci sertifikası ile bu adımları tooconfigure hello Web hizmeti SDK'sı izleyin.

1. Merhaba Web hizmeti SDK'sı çalıştıran hello sunucu için bir sertifika yetkilisinden bir istemci sertifikası alın. Nasıl çok öğrenin[istemci sertifikalarını alma](https://technet.microsoft.com/library/cc770328.aspx).  
2. İçeri aktarma hello istemci sertifikası toohello yerel bilgisayar kişisel sertifika deposuna hello Web hizmeti SDK'sı çalıştıran hello sunucusunda. Bu hello sertifika yetkilisinin genel sertifikasının güvenilen kök sertifikalar sertifika deposunda olduğundan emin olun.  
3. Merhaba ortak ve özel anahtarlarını hello istemci sertifika tooa .pfx dosyasına aktarın.  
4. Merhaba ortak anahtarı Base64 biçimi tooa .cer dosyasına aktarın.  
5. Sunucu Yöneticisi'nde bu hello Web sunucusu (IIS) \Web Server\Security\IIS istemci sertifikası eşleme kimlik doğrulaması özelliğinin yüklü doğrulayın. Yüklenmemişse, seçin **rol ve Özellik Ekle** tooadd bu özellik.  
6. IIS Yöneticisi'nde çift **yapılandırma Düzenleyicisi** hello Web hizmeti SDK'sı sanal dizinini içeren hello Web sitesinde. Bu önemli tooselect hello Web sitesi, sanal dizin hello olur.  
7. Toohello Git **system.webServer/security/authentication/iisClientCertificateMappingAuthentication** bölümü.  
8. Çok etkin kümesi**doğru**.  
9. OneToOneCertificateMappingsEnabled çok ayarlamak**doğru**.  
10. Merhaba tıklatın **...**  düğmesini sonraki toooneToOneMappings ve hello ardından **Ekle** bağlantı.  
11. Daha önce dışarı aktarılan hello Base64 .cer dosyasını açın. *-----BEGIN CERTIFICATE-----*, *-----END CERTIFICATE-----* ifadelerini ve tüm satır sonlarını kaldırın. Merhaba Sonuç dizesini kopyalayın.  
12. Set sertifika toohello dizesi adım önceki hello kopyalanır.  
13. Çok etkin kümesi**doğru**.  
14. Kullanıcı adı tooan hello PhoneFactor Admins güvenlik grubunun üyesi olan bir hesaba ayarlayın. Kullanım hello &lt;etki alanı&gt;&#92;&lt; Kullanıcı adı&gt; biçimi.  
15. Hello parola toohello uygun hesap parolasına ayarlayın ve ardından Yapılandırma Düzenleyicisi'ni kapatın.  
16. Merhaba tıklatın **Uygula** bağlantı.  
17. Merhaba Web hizmeti SDK'sı sanal dizininde, çift **kimlik doğrulama**.  
18. ASP.NET kimliğe bürünme ve temel kimlik doğrulaması çok ayarlandığını doğrulayın**etkin**, ve diğer tüm öğeleri çok ayarlandığını**devre dışı**.  
19. Merhaba Web hizmeti SDK'sı sanal dizininde, çift **SSL ayarları**.  
20. İstemci sertifikaları çok ayarlayın**kabul**ve ardından **Uygula**.  
21. Merhaba AD FS bağdaştırıcısı çalıştıran eski toohello server dışarı aktarılan hello .pfx dosyasını kopyalayın.  
22. Merhaba .pfx dosyası toohello yerel bilgisayar kişisel sertifika deposuna aktarın.  
23. Sağ tıklatıp **özel anahtarları Yönet**ve toohello AD FS hizmetinde toosign kullanılan sonra grant okuma erişimi toohello hesabı.  
24. Hello hello istemci sertifikası ve kopyalama hello parmak açmak **ayrıntıları** sekmesi.  
25. Merhaba MultiFactorAuthenticationAdfsAdapter.config dosyasında ayarlanan **WebServiceSdkCertificateThumbprint** toohello dize hello önceki adımda kopyaladığınız.  

Merhaba \Program Files\Multi çalıştırmak son olarak, tooregister hello bağdaştırıcısı-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1 betiğini PowerShell'de. Merhaba bağdaştırıcı WindowsAzureMultiFactorAuthentication olarak kaydedilir. Merhaba kayıt tootake etkisi Hello AD FS hizmetini yeniden başlatın.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>AD FS kullanarak Azure AD kaynaklarını güvenli hale getirme
toosecure, bulut kaynak kümesi bir talep kuralı böylece bir kullanıcı iki aşamalı doğrulamayı başarıyla gerçekleştirdiğinde, Active Directory Federasyon Hizmetleri hello multipleauthn talebi gösterir. Bu talep AD tooAzure üzerinde geçirilir. Bu yordam toowalk hello adımları izleyin:

1. AD FS Yönetimi'ni açın.
2. Merhaba solda seçin **bağlı olan taraf güvenleri**.
3. **Microsoft Office 365 Kimlik Platformu**’na sağ tıklayın ve **Talep Kurallarını Düzenle…** seçeneğini belirleyin

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Verme Dönüştürme Kuralları’nda **Kural Ekle**’ye tıklayın.

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. Açık dönüştürme talep Kuralı Ekleme Sihirbazı Merhaba, seçin **geçir veya Filtrele bir gelen talep** açılan hello ve'ı tıklatın **sonraki**.

   ![Bulut](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Kuralınıza bir ad verin.
7. Seçin **kimlik doğrulama yöntemleri başvuruları** hello gelen talep türü.
8. **Tüm talep değerlerini geçir**’i seçin.
    ![Dönüşüm Talep Kuralı Ekleme Sihirbazı](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. **Son**'a tıklayın. Merhaba AD FS Yönetim Konsolu'nu kapatın.

## <a name="related-topics"></a>İlgili konular
Sorun giderme Yardımı için bkz: Merhaba [Azure çok faktörlü kimlik doğrulaması ile ilgili SSS](multi-factor-authentication-faq.md)
