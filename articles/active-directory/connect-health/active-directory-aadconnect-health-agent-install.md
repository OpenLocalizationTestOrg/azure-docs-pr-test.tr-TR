---
title: "aaaAzure AD Connect Health Aracısı yüklemesi | Microsoft Docs"
description: "Bu, AD FS ve eşitleme için aracı yüklemesini hello açıklayan hello Azure AD Connect Health sayfasıdır."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9019628ec1d4c477496e08910cfd668ed1933a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a>Azure AD Connect Health Aracısı Yüklemesi
Bu belge yükleme ve hello Azure AD Connect Health aracıları yapılandırma anlatılmaktadır. Merhaba aracılardan indirebilirsiniz [burada](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent).

## <a name="requirements"></a>Gereksinimler
Aşağıdaki tablonun hello Azure AD Connect Health kullanma gereksinimleri listelenmiştir.

| Gereksinim | Açıklama |
| --- | --- |
| Azure AD Premium |Azure AD Connect Health, bir Azure AD Premium özelliği olup Azure AD Premium gerektirir. </br></br>Daha fazla bilgi için bkz. [Azure AD Premium ile Çalışmaya Başlama](../active-directory-get-started-premium.md) </br>Ücretsiz 30 günlük deneme toostart bakın [bir deneme başlatın.](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Bir genel olmalıdır, Azure AD tooget Yöneticisi Azure AD Connect Health ile başlatıldı |Varsayılan olarak, yalnızca hello genel yöneticiler yükleyebilir ve başlatıldı, hello sistem durumu aracısı tooget erişim hello portal, yapılandırma ve Azure AD Connect Health içinde hiçbir işlem gerçekleştiremezsiniz. Daha fazla bilgi için bkz. [Azure AD dizininizi yönetme](../active-directory-administer.md). <br><br> Rol tabanlı erişim denetimini kullanarak, erişim tooAzure AD Connect Health tooother kullanıcılar, kuruluşunuzda izin verebilirsiniz. Daha fazla bilgi için bkz. [Azure AD Connect Health için Rol Tabanlı Erişim Denetimi.](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) </br></br>**Önemli:** hello hello aracılarını yükleme bir iş veya Okul hesabı olmalıdır sırasında kullanılan hesap. Bir Microsoft hesabı olamaz. Daha fazla bilgi için bkz. [Azure'a kuruluş olarak kaydolma](../sign-up-organization.md) |
| Azure AD Connect Health Aracısı, hedeflenen tüm sunucularda yüklüdür | Azure AD Connect Health hello Health aracıları toobe yüklü ve hedeflenen sunucu tooreceive hello verileri üzerinde yapılandırılmış ve hello izleme ve analiz yetenekleri sağlamak gerektirir </br></br>Örneğin, hello Aracısı, AD FS altyapınızın tooget verilerden hello AD FS ve Web uygulaması Proxy sunucularının yüklenmesi gerekir. Benzer şekilde, şirket içi tooget verileri AD DS altyapı hello Aracısı hello etki alanı denetleyicileri üzerinde yüklü olmalıdır. </br></br> |
| Giden bağlantı toohello Azure hizmet uç noktaları | Yükleme ve çalışma zamanı sırasında hello Aracısı bağlantısı tooAzure AD Connect Health hizmet uç noktaları gerektirir. Güvenlik duvarları kullanarak giden bağlantı engellenirse uç noktaları aşağıdaki o hello toohello izin verilen listesine eklenen emin olun: </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.servicebus.windows.net - Bağlantı Noktası: 5671 </li><li>&#42;.adhybridhealth.azure.com/</li><li>https://management.azure.com </li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
|IP Adreslerini temel alan giden bağlantı | İçin IP adresi tabanlı güvenlik duvarları üzerinde filtreleme başvurun toohello [Azure IP aralıkları](https://www.microsoft.com/en-us/download/details.aspx?id=41653).|
| Giden trafik için SSL İncelemesi filtrelenmiş ya da devre dışı | SSL denetleme veya sonlandırma hello ağ katmanında giden trafik için ise hello aracı kayıt adım veya verileri karşıya yükleme işlemleri başarısız olabilir. |
| Merhaba Aracısı çalıştıran hello sunucusunda güvenlik duvarı bağlantı noktaları. |Merhaba aracının güvenlik duvarı bağlantı noktalarının toobe açık hello Aracısı toocommunicate hello Azure AD Health hizmet uç noktaları için sırayla aşağıdaki hello gerekir.</br></br><li>TCP bağlantı noktası 443</li><li>TCP bağlantı noktası 5671</li> |
| IE Artırılmış Güvenlik etkinse aşağıdaki Web siteleri hello izin ver |IE Artırılmış Güvenlik etkinse, ardından hello aşağıdaki Web sitelerine giderek toohave hello aracısı yüklü olan hello sunucusuna izin verilmelidir.</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>Kuruluşunuzda Azure Active Directory tarafından güvenilen Federasyon sunucusu Hello. Örnek: https://sts.contoso.com</li> |
|FIPS’yi devre dışı bırakma|FIPS, Azure AD Connect Health aracıları tarafından desteklenmez.|

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-fs"></a>Merhaba AD FS için Azure AD Connect Health aracısını yükleme
toostart Merhaba aracı yüklemesi, indirdiğiniz hello .exe dosyasına çift tıklayın. Merhaba ilk ekranda Yükle'yi tıklatın.

![Azure AD Connect Health'i doğrulama](./media/active-directory-aadconnect-health-requirements/install1.png)

Merhaba yükleme tamamlandıktan sonra Şimdi Yapılandır'ı tıklatın.

![Azure AD Connect Health'i doğrulama](./media/active-directory-aadconnect-health-requirements/install2.png)

Bu, bir PowerShell penceresi tooinitiate hello aracı kayıt işlemini başlatır. İstendiğinde, erişim tooperform Aracısı kaydı olan bir Azure AD hesabıyla oturum açın. Varsayılan olarak genel yönetici hesabı hello erişebilir.

![Azure AD Connect Health'i doğrulama](./media/active-directory-aadconnect-health-requirements/install3.png)

Oturum açtıktan sonra PowerShell işleme devam eder. İşlem tamamlandıktan sonra PowerShell'i kapatabilirsiniz ve hello yapılandırma tamamlanmış olur.

Bu noktada, hello Hizmetleri olmalıdır Aracısı otomatik olarak izin verme hello Aracısı karşıya yükleme gerekli hello veri toohello bulut hizmeti güvenli bir şekilde başlatıldı.

Merhaba önceki bölümlerde belirtilen tüm hello ön koşullar karşılanmadığı takdirde uyarılar hello PowerShell penceresinde görünür. Emin toocomplete hello olması [gereksinimleri](active-directory-aadconnect-health-agent-install.md#requirements) hello aracı yüklemeden önce. Aşağıdaki ekran görüntüsü hello bu hataların bir örnektir.

![Azure AD Connect Health'i doğrulama](./media/active-directory-aadconnect-health-requirements/install4.png)

tooverify hello aracısı yüklü, hello sunucudaki hizmetler aşağıdaki hello arayın. Merhaba yapılandırmayı tamamladıysanız zaten çalışmalıdır. Merhaba yapılandırma tamamlanıncaya kadar Aksi halde, durdurulmuş.

* Azure AD Connect Health AD FS Tanılama Hizmeti
* Azure AD Connect Health AD FS Öngörü Hizmeti
* Azure AD Connect Health AD FS İzleme Hizmeti

![Azure AD Connect Health'i doğrulama](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>Windows Server 2008 R2 Sunucularında aracı yüklemesi
Windows Server 2008 R2 sunucuları için adımlar:

1. Bu hello server Service Pack 1 veya daha yüksek çalıştığından emin olun.
2. Aracı yüklemesi için IE ESC'yi devre dışı bırakın:
3. Merhaba AD Health aracısını yükleme öncesinde hello sunucuların her birinde Windows PowerShell 4.0 sürümünü yükleyin. Windows PowerShell 4.0 tooinstall:
   * Yükleme [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779) bağlantı toodownload hello çevrimdışı Yükleyici aşağıdaki hello kullanarak.
   * PowerShell ISE'yi yükleme (Windows Özelliklerinden)
   * Merhaba yüklemek [Windows Management Framework 4.0.](https://www.microsoft.com/download/details.aspx?id=40855)
   * Internet Explorer sürüm 10 veya üstü hello sunucusunda. (Azure yönetici kimlik bilgilerinizi kullanarak hello sistem durumu hizmeti tooauthenticate tarafından gereklidir.)
4. Windows Server 2008 R2'de Windows PowerShell 4.0 sürümünü yükleme hakkında daha fazla bilgi için hello wiki makalesine bakın [burada](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx).

### <a name="enable-auditing-for-ad-fs"></a>AD FS için Denetimi Etkinleştirme
> [!NOTE]
> Bu bölüm, yalnızca tooAD FS sunucuları geçerlidir. Merhaba Web Uygulama Proxy sunucuları üzerinde aşağıdaki adımları toofollow sahip değil.
>

Kullanım analizi toogather özellik ve analiz hello sırayla verileri, hello Azure AD Connect Health Aracısı hello AD FS denetim günlüklerini bilgilerinde hello. Bu günlükler varsayılan olarak etkin değildir. Kullanım hello tooenable AD FS denetim yordamları izleyerek ve toolocate hello AD FS denetim günlükleri, AD FS sunucularınızda.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2008-r2"></a>Windows Server 2008 R2 üzerinde AD FS için tooenable denetleme
1. Tıklatın **Başlat**, çok noktası**programları**, çok noktası**Yönetimsel Araçlar**ve ardından **yerel güvenlik ilkesi**.
2. Toohello gidin **Güvenlik Ayarları\Yerel İlkeler\Kullanıcı Hakları Yönetimi** klasörünü ve güvenlik denetimleri oluştur çift tıklatın.
3. Merhaba üzerinde **yerel güvenlik ayarları** sekmesinde, başlangıç AD FS 2.0 hizmet hesabının listelenmiş olduğunu doğrulayın. Mevcut değilse tıklatın **kullanıcı veya Grup Ekle** toohello listeye ekleyin ve ardından **Tamam**.
4. tooenable denetleme, yükseltilmiş ayrıcalıklarla bir komut istemi açın ve hello aşağıdaki komutu çalıştırın:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. Yerel Güvenlik İlkesi kapatın ve hello Yönetimi ek bileşenini açın. Yönetimi ek bileşenini, tooopen hello tıklatın **Başlat**, çok noktası**programları**, çok noktası**Yönetimsel Araçlar**ve ardından AD FS 2.0 yönetimi.
6. Merhaba Eylemler bölmesinde, Federasyon Hizmeti özelliklerini Düzenle'yi tıklatın.
7. Merhaba, **Federasyon Hizmeti özelliklerini** iletişim kutusunda, hello **olayları** sekmesi.
8. Select hello **başarı denetimleri** ve **hata denetimleri** onay kutuları.
9. **Tamam** düğmesine tıklayın.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>Windows Server 2012 R2 AD FS için tooenable denetleme
1. Açık **yerel güvenlik ilkesi** açarak **Sunucu Yöneticisi'ni** hello başlangıç ekranında veya Sunucu Yöneticisi'nde hello Masaüstü hello çubuğunda, ardından **Araçlar/yerel güvenlik ilkesi**.
2. Toohello gidin **Güvenlik Ayarları\Yerel İlkeler\Kullanıcı Hakları Ataması** klasörü ve çift tıklatarak **güvenlik denetimleri oluştur**.
3. Merhaba üzerinde **yerel güvenlik ayarları** sekmesinde, başlangıç AD FS hizmet hesabının listelenmiş olduğunu doğrulayın. Mevcut değilse tıklatın **kullanıcı veya Grup Ekle** toohello listeye ekleyin ve ardından **Tamam**.
4. tooenable denetleme, yükseltilmiş ayrıcalıklarla bir komut istemi açın ve hello aşağıdaki komutu çalıştırın: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```.
5. Kapat **yerel güvenlik ilkesi**ve ardından hello açın **AD FS Yönetimi** ek bileşenini (Sunucu Yöneticisi ' nde Araçlar'ı tıklatın ve ardından AD FS Yönetimi'ni seçin).
6. Merhaba Eylemler bölmesinde **Federasyon Hizmeti özelliklerini Düzenle**.
7. Merhaba Hello Federasyon Hizmeti Özellikleri iletişim kutusunda tıklatın **olayları** sekmesi.
8. Select hello **başarı denetimleri ve hata denetimleri** onay kutularını işaretleyin ve ardından **Tamam**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2016"></a>AD FS Windows Server 2016 için tooenable denetleme
1. Açık **yerel güvenlik ilkesi** açarak **Sunucu Yöneticisi'ni** hello başlangıç ekranında veya Sunucu Yöneticisi'nde hello Masaüstü hello çubuğunda, ardından **Araçlar/yerel güvenlik ilkesi**.
2. Toohello gidin **Güvenlik Ayarları\Yerel İlkeler\Kullanıcı Hakları Ataması** klasörü ve çift tıklatarak **güvenlik denetimleri oluştur**.
3. Merhaba üzerinde **yerel güvenlik ayarları** sekmesinde, başlangıç AD FS hizmet hesabının listelenmiş olduğunu doğrulayın. Mevcut değilse tıklatın **kullanıcı veya Grup Ekle** hello AD FS hizmet hesabı toohello listeye ekleyin ve ardından **Tamam**.
4. tooenable denetleme, yükseltilmiş ayrıcalıklarla bir komut istemi açın ve hello aşağıdaki komutu çalıştırın:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. Kapat **yerel güvenlik ilkesi**ve ardından hello açın **AD FS Yönetimi** ek bileşenini (Sunucu Yöneticisi ' nde Araçlar'ı tıklatın ve ardından AD FS Yönetimi'ni seçin).
6. Merhaba Eylemler bölmesinde **Federasyon Hizmeti özelliklerini Düzenle**.
7. Merhaba Hello Federasyon Hizmeti Özellikleri iletişim kutusunda tıklatın **olayları** sekmesi.
8. Select hello **başarı denetimleri ve hata denetimleri** onay kutularını işaretleyin ve ardından **Tamam**. Bu seçenek varsayılan olarak etkindir.
9. Bir PowerShell penceresi açın ve hello aşağıdaki komutu çalıştırın: ```Set-AdfsProperties -AuditLevel Verbose```.

"Temel" denetim düzeyi varsayılan olarak etkindir. Merhaba hakkında daha fazla bilgiyi [Windows Server 2016 AD FS denetim geliştirme](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)


#### <a name="toolocate-hello-ad-fs-audit-logs"></a>toolocate hello AD FS denetim günlükleri
1. **Olay Görüntüleyicisi**'ni açın.
2. TooWindows günlükleri gidip seçin **güvenlik**.
3. Sağ Hello üzerinde tıklatın **filtresi geçerli günlükleri**.
4. Event Source (Olay Kaynağı) altındaki **AD FS Auditing (AD FS Denetimi)** seçeneğini belirleyin.

![AD FS denetim günlükleri](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> AD FS denetimi bir grup ilkesiyle devre dışı bırakılabilir. AD FS denetimi devre dışı bırakılırsa, oturum açma etkinlikleriyle ilgili kullanım analizi mevcut olmaz. AD FS denetimini devre dışı bırakan bir grup ilkesine sahip olmadığınızdan emin olun.>
>


## <a name="installing-hello-azure-ad-connect-health-agent-for-sync"></a>Eşitleme için Hello Azure AD Connect Health aracısını yükleme
Hello Azure AD Connect Health aracısını eşitleme için Azure AD Connect hello son sürüme otomatik olarak yüklenir. toouse Azure AD Connect eşitleme, Azure AD Connect toodownload hello en son sürümü gerekir ve yükleyin. Merhaba en son sürümünü indirebilirsiniz [burada](http://www.microsoft.com/download/details.aspx?id=47594).

tooverify hello aracısı yüklü, hello sunucudaki hizmetler aşağıdaki hello arayın. Merhaba yapılandırmayı tamamladıysanız zaten çalışmalıdır. Merhaba yapılandırma tamamlanıncaya kadar Aksi halde, durdurulmuş.

* Azure AD Connect Health Eşitleme Öngörü Hizmeti
* Azure AD Connect Health Eşitleme İzleme Hizmeti

![Eşitleme için Azure AD Connect Health'i doğrulama](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> Azure AD Connect Health'in kullanılabilmesi için Azure AD Premium'un gerekli olduğunu unutmayın. Azure AD Premium yoksa oluşturulamıyor toocomplete hello yapılandırma hello Azure portal'ın verilmiştir. Daha fazla bilgi için bkz: Merhaba [gereksinimler sayfası](active-directory-aadconnect-health-agent-install.md#requirements).
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>El ile Eşitleme için Azure AD Connect Health kaydı
Hello Azure AD Connect Health eşitleme Aracısı kaydı için Azure AD Connect'i başarıyla yükledikten sonra başarısız olursa, aşağıdaki PowerShell komutunu toomanually kaydetmek hello Aracısı hello kullanabilirsiniz.

> [!IMPORTANT]
> Bu PowerShell komutunu kullanarak, yalnızca hello aracı kaydı Azure AD Connect yüklendikten sonra başarısız olursa gereklidir.
>
>

Merhaba aşağıdaki PowerShell komutunu yalnızca hello durum Aracısı kaydının bile başarılı yüklemesinden ve Azure AD Connect yapılandırma sonra başarısız olursa gereklidir. hello Azure AD Connect Health Hizmetleri Hello Aracısı başarıyla kaydedildikten sonra başlar.

Merhaba aşağıdaki PowerShell komutunu kullanarak eşitleme için hello Azure AD Connect Health aracısını el ile kaydedebilirsiniz:

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

Merhaba komutu parametreleri alır:

* AttributeFiltering: $true (varsayılan) - Azure AD Connect hello varsayılan öznitelik kümesi eşitlemiyor ve filtrelenmiş bir öznitelik özelleştirilmiş toouse olup olmadığını belirleyin. Aksi halde $false değerini alır.
* StagingMode: $false (varsayılan) - hello Azure AD Connect sunucusu hello sunucusuysa hazırlama modu, $true içinde değilse, hazırlama modunda toobe yapılandırılmış.

Kimlik doğrulaması için istendiğinde kullanması gereken hello aynı genel yönetici hesabını (gibi admin@domain.onmicrosoft.com) Azure AD Connect'in yapılandırılması için kullanıldı.

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-ds"></a>Merhaba AD DS için Azure AD Connect Health aracısını yükleme
toostart Merhaba aracı yüklemesi, indirdiğiniz hello .exe dosyasına çift tıklayın. Merhaba ilk ekranda Yükle'yi tıklatın.

![Azure AD Connect Health'i doğrulama](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

Merhaba yükleme tamamlandıktan sonra Şimdi Yapılandır'ı tıklatın.

![Azure AD Connect Health'i doğrulama](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

Bir komut istemi başlatılır ve ardından bazı PowerShell uygulamaları tarafından Register-AzureADConnectHealthADDSAgent komutu yürütülür. İstendiğinde toosign tooAzure içinde Git şimdi ne zaman ve oturum açın.

![Azure AD Connect Health'i doğrulama](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

Oturum açtıktan sonra PowerShell işleme devam eder. İşlem tamamlandıktan sonra PowerShell'i kapatabilirsiniz ve hello yapılandırma tamamlanmış olur.

Bu noktada, hello hizmetleri otomatik olarak hello Aracısı toomonitor izin vererek başlatılmalıdır ve verileri toplayın. Merhaba önceki bölümlerde belirtilen tüm hello ön koşullar karşılanmadığı takdirde uyarılar hello PowerShell penceresinde görünür. Emin toocomplete hello olması [gereksinimleri](active-directory-aadconnect-health-agent-install.md#requirements) hello aracı yüklemeden önce. Aşağıdaki ekran görüntüsü hello bu hataların bir örnektir.

![AD DS için Azure AD Connect Health'i doğrulama](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

tooverify hello aracısı yüklü, hizmetleri hello etki alanı denetleyicisinde aşağıdaki hello arayın.

* Azure AD Connect Health AD DS Insights Hizmeti
* Azure AD Connect Health AD DS İzleme Hizmeti

Merhaba yapılandırmayı tamamladıysanız hizmetlerin zaten çalıştırması gerekir. Merhaba yapılandırma tamamlanıncaya kadar Aksi halde, durdurulmuş.

![Azure AD Connect Health'i doğrulama](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a>PowerShell kullanarak Aracı Kaydı
Merhaba uygun Aracısı setup.exe yükledikten sonra hello aracı kayıt adımı PowerShell komutlarını hello rolüne bağlı olarak aşağıdaki hello kullanarak gerçekleştirebilirsiniz. Bir PowerShell penceresi açın ve hello uygun komutu çalıştırın:

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

Bu komutları "Kimlik" Etkileşimli olmayan bir şekilde ya da bir sunucu çekirdeği makinede bir parametre toocomplete hello kayıt olarak kabul eder.
* Merhaba kimlik bilgileri, bir parametre olarak geçirilen PowerShell değişkeninde yakalanır.
* Erişim tooregister hello aracıları ve MFA etkin olmayan tüm Azure AD Identity sağlayabilir.
* Varsayılan olarak genel yönetici erişimi tooperform aracı kaydı. Ayrıca diğer daha az ayrıcalıklı kimlikleri tooperform bu adımı izin verebilirsiniz. [Rol Tabanlı Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) hakkında daha fazla bilgi edinin.

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-toouse-http-proxy"></a>Azure AD Connect Health aracılarını toouse HTTP proxy'sini yapılandırma
Bir HTTP Proxy'si ile Azure AD Connect Health aracılarını toowork yapılandırabilirsiniz.

> [!NOTE]
> * Hello aracı Microsoft Windows HTTP Hizmetleri yerine System.Net toomake web istekleri kullandığından "Netsh WinHttp set proxyserveraddress" kullanımı desteklenmiyor.
> * Merhaba yapılandırılan Http proxy'si kullanılan toopass aracılığıyla şifrelenmiş Https iletilerinin adresidir.
> * HTTPBasic kullanılarak kimliği doğrulanmış ara sunucular desteklenmez.
>
>

### <a name="change-health-agent-proxy-configuration"></a>Durum Aracısı Ara Sunucu Yapılandırmasını Değiştirme
Seçenekler tooconfigure Azure AD Connect Health Aracısı toouse bir HTTP Proxy aşağıdaki hello var.

> [!NOTE]
> Tüm Azure AD Connect Health Aracısı hizmetleri, güncelleştirilmiş hello proxy ayarları toobe sırayla yeniden başlatılması gerekir. Merhaba aşağıdaki komutu çalıştırın:<br>
> Restart-Service AdHealth*
>
>

#### <a name="import-existing-proxy-settings"></a>Var olan ara sunucu Ayarlarını içeri aktarma
##### <a name="import-from-internet-explorer"></a>Internet Explorer'dan içeri aktarma
Internet Explorer HTTP proxy ayarlarını aktarılabilir, toobe Azure AD Connect Health aracılarını hello tarafından kullanılır. Sunucuların her birinde hello durum aracısını çalıştıran Merhaba, PowerShell komutunu aşağıdaki hello yürütün:

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>WinHTTP'den içeri aktarma
WinHTTP proxy ayarları aktarılabilir, toobe Azure AD Connect Health aracılarını hello tarafından kullanılır. Sunucuların her birinde hello durum aracısını çalıştıran Merhaba, PowerShell komutunu aşağıdaki hello yürütün:

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>Ara sunucu adreslerini el ile belirtme
Merhaba aşağıdaki PowerShell komutunu yürüterek hello sistem durumu aracısı çalıştıran hello sunucuların her birinde bir proxy sunucusu el ile belirtebilirsiniz:

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

Örnek: *Set-AzureAdConnectHealthProxySettings - HttpsProxyAddress myproxyserver: 443*

* "adres", DNS'nin çözümlenebileceği bir sunucu adı veya bir IPv4 adresi olabilir.
* "bağlantı noktası" atlanabilir. Atlanması durumunda varsayılan bağlantı noktası olarak 443 seçilir.

#### <a name="clear-existing-proxy-configuration"></a>Var olan ara sunucu yapılandırmasını silme
Merhaba aşağıdaki komutu çalıştırarak hello mevcut proxy yapılandırmasını silebilirsiniz:

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>Geçerli ara sunucu ayarlarını okuma
Merhaba aşağıdaki komutu çalıştırarak şu anda yapılandırılmış hello proxy ayarlarını okuyabilirsiniz:

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-tooazure-ad-connect-health-service"></a>Test bağlantısı tooAzure AD Connect Health hizmeti
Sorunları hello Azure AD Connect Health Aracısı toolose bağlantı hello Azure AD Connect Health hizmeti ile neden kaynaklanabilecek mümkündür. Ağ sorunları, izin sorunları veya diğer çeşitli nedenler bunlara dahildir.

Merhaba Aracısı yüklenemiyor toosend veri toohello Azure AD Connect Health hizmeti iki saat daha uzun ise, uyarı hello Portalı'nda aşağıdaki hello ile belirtilir: "sistem sağlığı hizmeti verileri değil toodate." Merhaba aşağıdaki PowerShell komutunu çalıştırarak etkilenen hello Azure AD Connect Health Aracısı mümkün tooupload veri toohello Azure AD Connect Health hizmeti olup olmadığını doğrulayabilirsiniz:

    Test-AzureADConnectHealthConnectivity -Role ADFS

Merhaba rol parametresi şu anda değerleri aşağıdaki hello alır:

* ADFS
* Sync
* EKLER

Merhaba komutu tooview hello - ShowResults bayrağını kullanabilirsiniz ayrıntılı günlükleri. Aşağıdaki örnek hello kullan:

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> toouse hello bağlantı aracını, ilk tam hello aracı kaydı gerekir. Mümkün toocomplete hello aracı kaydı olmayan tüm hello karşıladığınızdan emin olun [gereksinimleri](active-directory-aadconnect-health-agent-install.md#requirements) Azure AD Connect Health için. Bu bağlantı testi, aracı kaydı sırasında varsayılan olarak gerçekleştirilir.
>
>

## <a name="related-links"></a>İlgili bağlantılar
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health İşlemleri](active-directory-aadconnect-health-operations.md)
* [Azure AD Connect Health'i AD FS ile Kullanma](active-directory-aadconnect-health-adfs.md)
* [Eşitleme için Azure AD Connect Health'i kullanma](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health'i AD DS ile Kullanma](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health ile ilgili SSS](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health Sürüm Geçmişi](active-directory-aadconnect-health-version-history.md)
