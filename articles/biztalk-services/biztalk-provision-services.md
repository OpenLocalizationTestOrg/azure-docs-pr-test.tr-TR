---
title: hello Azure portal, Azure BizTalk Services aaaCreate | Microsoft Docs
description: "Bilgi nasıl tooprovision veya hello Azure portalı; Azure BizTalk Services oluşturma MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a>Hello Azure portalını kullanarak BizTalk Services oluşturma

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> toosign toohello Azure portal'ın bir Azure hesabı ve Azure aboneliği gerekir. Hesabınız yoksa birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Bkz. [Azure Ücretsiz Deneme](http://go.microsoft.com/fwlink/p/?LinkID=239738).


## <a name="CreateService"></a>BizTalk Hizmeti oluşturma
Seçtiğiniz sürüm Hello bağlı olarak, tüm BizTalk hizmeti ayarlarını bulunabilir.

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Merhaba alt Gezinti bölmesinde seçin **yeni**:  
   ![Merhaba yeni düğmesini seçme][NEWButton]
3. **UYGULAMA HİZMETLERİ** > **BIZTALK HİZMETİ** > **ÖZEL OLUŞTUR**’u seçin:  
   ![BizTalk Hizmeti’ni seçin ve Özel Oluştur’u seçin][NewBizTalkService]
4. Merhaba BizTalk hizmeti ayarlarını girin:
   
    <table border="1">
    <tr>
    <td><strong>BizTalk hizmeti adı</strong></td>
    <td>Herhangi bir ad girin, ancak özel olsun. Bazı örnekler:<br/><br/>
    <em>şirketim</em>.biztalk.windows.net<br/>
    <em>şirketimuygulamam</em>.biztalk.windows.net<br/>
    <em>uygulamam</em>.biztalk.windows.net<br/><br/>". biztalk.windows.net" girdiğiniz otomatik olarak eklenen toohello adıdır. Bu gibi BizTalk hizmeti kullanılan tooaccess bir URL oluşturur <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>.
    </td>
    </tr>
    <tr>
    <td><strong>Sürüm</strong></td>
    <td>Merhaba test/geliştirme aşamasındaysanız seçin <strong>Geliştirici</strong>. Merhaba üretim aşamasında, hello kullanırsanız <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: sürümler grafiği</a> toodetermine varsa <strong>Premium</strong>, <strong>standart</strong>, veya <strong>Basic</strong>, iş senaryonuz için hello doğru seçimdir.
    </td>
    </tr>
    <tr>
    <td><strong>Bölge</strong></td>
    <td>Merhaba coğrafi bölge toohost BizTalk hizmetinizi seçin.</td>
    </tr>
    <tr>
    <td><strong>Etki alanı URL'si</strong></td>
    <td><strong>İsteğe bağlı</strong>. Varsayılan olarak, hello etki alanı URL'dir <em>YourBizTalkServiceName</em>. biztalk.windows.net. Özel bir etki alanı da girilebilir. Örneğin, etki alanınız <em>contoso</em> olarak belirtilmişse şunları girebilirsiniz: <br/><br/>
    <em>Şirketim</em>.contoso.com<br/>
    <em>ŞirketimUygulamam</em>.contoso.com<br/>
    <em>Uygulamam</em>.contoso.com<br/>
    <em>BizTalkHizmetAdınız</em>.contoso.com<br/>
    </td>
    </tr>
    </table>
Merhaba İleri okunu seçin.
5. Merhaba depolama ve veritabanı ayarlarını girin:  <table border="1">
    <tr>
    <td><strong>Depolama hesabını izleme/arşivleme</strong></td>
    <td>Mevcut bir depolama hesabını seçin veya yeni bir depolama hesabı oluşturun. <br/><br/>Yeni bir depolama hesabı oluşturursanız, hello girin <strong>depolama hesabı adı</strong>.</td>
    </tr>
    <tr>
    <td><strong>Veritabanı izleme</strong></td>
    <td>Mevcut bir Azure SQL veritabanı kullanıyorsanız, başka bir BizTalk hizmeti tarafından kullanılamaz. Merhaba oturum açma adı ve parola, Azure SQL veritabanı sunucusu oluşturulduğunda girilen gerekir.<br/><br/><strong>İpucu</strong> hello izleme veritabanı oluşturma ve izleme/arşivleme depolama hesabında BizTalk hizmeti hello gibi aynı bölgede hello.</td>
    </tr>
    </table>
Merhaba İleri okunu seçin.
6. Merhaba veritabanı ayarlarını girin:  <table border="1">
    <tr>
    <td><strong>Ad</strong></td>
    <td>Kullanılabilir olduğunda <strong>yeni bir SQL veritabanı oluştur</strong> hello önceki ekrana seçilir.
    <br/><br/>
BizTalk hizmeti tarafından kullanılan bir SQL veritabanı adı toobe girin.</td>
    </tr>
    <tr>
    <td><strong>Sunucu</strong></td>
    <td>Kullanılabilir olduğunda <strong>yeni bir SQL veritabanı oluştur</strong> hello önceki ekrana seçilir.
    <br/><br/>
Mevcut bir SQL Database Sunucusu seçin veya yeni bir SQL Database sunucusu oluşturun.</td>
    </tr>
    <tr>
    <td><strong>Sunucu oturum açma adı</strong></td>
    <td>Merhaba oturum açma kullanıcı adı girin.</td>
    </tr>
    <tr>
    <td><strong>Sunucu oturum açma parolası</strong></td>
    <td>Merhaba oturum açma parolasını girin.</td>
    </tr>
    <tr>
    <td><strong>Bölge</strong></td>
    <td><strong>Yeni bir SQL veritabanı oluştur</strong> seçili olduğunda kullanılabilir. Merhaba coğrafi bölge toohost SQL veritabanınızı seçin.</td>
    </tr>
    </table>

Merhaba onay işareti toocomplete hello Sihirbazı'nı seçin. Merhaba ilerleme simgesi görünür:  
![Tamamlandığında ilerleme simgesi görüntülenir][ProgressComplete]

Tamamlandığında, Azure BizTalk hizmeti hello oluşturulan ve uygulamalarınız için hazır olur. Merhaba varsayılan ayarlar yeterlidir. Toochange hello varsayılan ayarları istiyorsanız seçin **BIZTALK SERVICES** sol gezinti bölmesinde hello ve BizTalk hizmetinizi seçin. Ek ayarlar hello görüntülenir [Pano, İzleyici ve ölçek sekmeleri](biztalk-dashboard-monitor-scale-tabs.md) hello üstünde.

Merhaba BizTalk hizmeti Hello durumuna bağlı olarak, tamamlanamıyor bazı işlemler vardır. Bu işlemlerin bir listesi için çok Git[BizTalk Services durumu grafiği](biztalk-service-state-chart.md).

## <a name="post-provisioning-steps"></a>Hazırlama sonrası adımlar
* [Yerel bir bilgisayara Hello sertifika yükleme](#InstallCert)
* [Üretime hazır sertifikayı ekleme](#AddCert)
* [Merhaba erişim denetimi ad alanını alma](#ACS)

#### <a name="InstallCert"></a>Yerel bir bilgisayara Hello sertifika yükleme
BizTalk Hizmeti hazırlamanın bir parçası olarak, otomatik olarak imzalanan ve BizTalk hizmeti aboneliğinizle ilişkili bir sertifika oluşturulur. Bu sertifikayı indirip burada BizTalk hizmeti uygulamalarını dağıtacağınız ya da iletileri tooa BizTalk Hizmeti uç noktası Gönder bilgisayarların yüklemeniz gerekir.

1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Seçin **BIZTALK SERVICES** sol gezinti bölmesinde hello ve BizTalk hizmeti aboneliğinizi seçin.
3. Select hello **Pano** sekmesi.
4. **SSL Sertifikası İndir**’i seçin:  
   ![SSL Sertifikasını Değiştirme][QuickGlance]
5. Merhaba sertifikayı çift tıklatın ve hello Sihirbazı tooinstall hello sertifika üzerinden çalıştırın. Merhaba altına hello sertifikayı yüklediğinizden emin olun **güvenilen kök sertifika yetkilileri** depolar.

#### <a name="AddCert"></a>Üretime hazır sertifikayı ekleme
BizTalk Services oluşturma yalnızca geliştirme ortamlarında kullanılmak üzere tasarlanmıştır otomatik olarak oluşturulan hello otomatik olarak imzalanan sertifika. Üretim senaryoları için üretime hazır sertifikayla değiştirin.

1. Merhaba üzerinde **Pano** sekmesine **SSL sertifikasını Güncelleştir**.
2. Tooyour özel SSL sertifikasına göz atın (*CertificateName*.pfx), BizTalk hizmeti adını içeren, hello parolayı girin ve ardından hello onay işaretine tıklayın.

#### <a name="ACS"></a>Merhaba erişim denetimi ad alanını alma
1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Seçin **BIZTALK SERVICES** sol gezinti bölmesinde hello ve BizTalk hizmetinizi seçin.
3. Merhaba görev çubuğunda seçin **bağlantı bilgilerini**:  
   ![Bağlantı Bilgilerini seçme][ACSConnectInfo]
4. Merhaba erişim denetimi değerlerini kopyalayın.

Visual Studio’dan BizTalk Hizmeti projesini dağıttığınızda, Erişim Denetimi ad alanına bunu girin. Merhaba erişim denetimi ad alanı BizTalk hizmetiniz için otomatik olarak oluşturulur.

Merhaba erişim denetimi değerleri herhangi bir uygulama ile kullanılabilir. Azure BizTalk Services oluşturulduğunda, bu erişim denetimi ad alanı BizTalk hizmeti dağıtımınız ile Merhaba kimlik doğrulaması denetler. Toochange hello abonelik veya hello ad alanını yönetmek istiyorsanız seçin **ACTIVE DIRECTORY** sol gezinti bölmesinde hello ve sonra da ad alanınızı seçin. Merhaba görev çubuğu seçeneklerinizi listeler.

Tıklatarak **Yönet** açılır hello erişim denetimi Yönetim Portalı. Hello erişim denetimi Yönetim Portalı'da, BizTalk hizmeti kullanan hello **hizmet kimliklerini**:  
![Merhaba erişim denetimi Yönetim Portalı'nda ACS hizmet kimlikleri][ACSServiceIdentities]

Merhaba erişim denetimi hizmeti kimliği, uygulamaların veya istemcilerin tooauthenticate erişim denetimi ile doğrudan izin vermek ve bir belirteç almalarına kimlik bilgileri kümesidir.

> [!IMPORTANT]
> Merhaba BizTalk hizmeti kullanan **sahibi** hello varsayılan hizmet kimliği ve hello **parola** değeri. Parola değeri hello yerine hello simetrik anahtar değeri kullanırsanız hello aşağıdaki hata oluşabilir.<br/><br/>*Belirtilen hello ile toohello erişim denetimi yönetim hizmeti hesabına bağlanılamadı kimlik bilgileri*
> 
> 

[ACS Ad Alanınızı Yönetme](https://msdn.microsoft.com/library/azure/hh674478.aspx) bazı kılavuzları ve önerileri listeler.

## <a name="requirements-explained"></a>Açıklanan gereksinimler
Bu gereksinimleri toohello uygulamayın ücretsiz sürüm.

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>Ne gerekiyor?</strong></td>
        <td><strong>Neden gerekiyor?</strong></td>
</tr>
<tr>
<td>Azure aboneliği</td>
<td>Merhaba abonelik toohello Azure portalında oturum açarak belirler. Merhaba hesap sahibi oluşturur hello aboneliğinizi <a HREF="https://account.windowsazure.com/Subscriptions"> Azure abonelikleri</a>.
<br/><br/>
Hello Azure hesabı birden fazla abonelik olabilir ve izin herkes tarafından yönetilebilir. Örneğin, Azure hesap sahibi adlı bir abonelik oluşturulur <em>BizTalkServiceSubscription</em> ve sağlar, şirket BizTalk yöneticileri hello (örneğin, ContosoBTSAdmins@live.com) erişim toothis abonelik. Bu senaryoda, hello BizTalk Yöneticiler toohello Azure portalında oturum açın ve Azure BizTalk Services de dahil olmak üzere hello abonelikte tam yönetici hakları tooall hello barındırılan hizmetleri sahiptir. Merhaba BizTalk yöneticileri hello Azure hesap sahipleri değildir ve bu nedenle erişim tooany faturalama bilgileri yok.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Hello Azure portalında abonelikleri ve depolama hesaplarını yönetecek</a> daha fazla bilgi sağlar.
</td>
</tr>
<tr>
<td>Azure SQL Database</td>
<td>Merhaba tabloları, görünümleri ve saklı yordamlar hello hello izleme verileri de dahil olmak üzere, BizTalk hizmeti tarafından kullanılan depolar.
<br/><br/>
BizTalk Hizmeti oluşturduğunuzda, mevcut Azure SQL Sunucusu, Azure SQL Database kullanırsınız ya da otomatik olarak yeni bir Sunucu veya SQL Database oluşturursunuz.
<br/><br/>
Merhaba SQL Database ölçeği otomatik olarak yapılandırılır. Genellikle, hello varsayılan ölçek BizTalk hizmeti için yeterlidir. Değişen hello ölçek fiyatı etkiler. Bkz. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Azure SQL Veritabanı'nda Hesaplar ve Faturalar</a>
<br/><br/>
<strong>Notlar</strong>
<br/>
<ul>
<li> Yeni bir Azure SQL sunucusu ve SQL Database oluşturduğunuzda, Azure Hizmetleri otomatik olarak etkinleşir. Merhaba BizTalk hizmeti gerektirir Azure Hizmetleri etkin olmalıdır.</li>
<li>Mevcut bir Azure SQL sunucusunda yeni bir Azure SQL veritabanı oluşturursanız, güvenlik duvarı kuralları sunucu değişmez hello hello. Sonuç olarak, diğer Azure hizmetlerine erişim toohello sunucunun veritabanlarına izin verilmiyor mümkündür.</li>
</ul>
</td>
</tr>
<tr>
<td>Azure Erişim Denetimi ad alanı</td>
<td>Azure BizTalk Services ile kimlik doğrular. Visual Studio’dan BizTalk Hizmeti projesini dağıttığınızda, Erişim Denetimi ad alanına bunu girin. BizTalk hizmeti oluşturduğunuzda, hello erişim denetimi ad alanı otomatik olarak oluşturulur.</td>
</tr>

<tr>
<td>Azure Storage hesabı</td>
<td>Tootables, BLOB'ları ve kuyrukları, BizTalk hizmeti toosave hello aşağıdaki tarafından kullanılan erişim izni verir:

<ul>
<li>Bu İzleyici hello BizTalk hizmeti günlük dosyaları. Çıktı izleme hello hello de görüntülenir **izleme** hello Azure portal sekmesindedir.</li>
<li>Bir X12 veya AS2 sözleşmesi iş ortakları arasında oluştururken hello arşivleme özelliğini toostore ileti özelliklerini etkinleştirebilirsiniz. Bu veriler hello depolama hesabı kaydedilir.</li>
</ul>
<br/>
BizTalk hizmeti oluşturduğunuzda, mevcut bir Storage hesabını kullanabilir ya da otomatik olarak yeni bir Storage hesabı oluşturabilirsiniz.
<br/><br/>
Merhaba varsayılan Storage ayarları BizTalk hizmeti için yeterlidir.
<br/><br/>
Storage hesabı oluşturduğunuzda, Birincil ve İkincil Anahtar da otomatik olarak oluşur. Bu anahtarları depolama hesabı erişim tooyour denetler. Merhaba BizTalk hizmeti otomatik olarak hello birincil anahtarı kullanır.
<br/><br/>
Daha fazla bilgi için bkz. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Storage</a>.
</td>
</tr>

<tr>
<td>SSL özel sertifikası</td>
<td>
Azure BizTalk Hizmeti oluşturulduğunda, BizTalk hizmeti adını içeren bir HTTPS URL'si de oluşturulur. Otomatik olarak yapılandırılan toouse otomatik olarak imzalanan salt geliştirme sertifikasını URL'dir. Üretim için özel bir SSL sertifikası gerekir.
<br/><br/>
<strong>Önemli SSL Sertifikası Bilgileri</strong>

<ul>
<li>Merhaba sertifika sona erme tarihi 5 yıldan az olmalıdır.</li>
<li>Tüm özel sertifikaları için parola gerekir. Bu parolayı öğrenin ve en iyisi bu parolayı yöneticilerinizle paylaşın.</li>
<li>Otomatik olarak imzalanan sertifikalar test/geliştirme ortamında kullanılır. Otomatik olarak imzalanan sertifikalar kullanıldığında hello sertifika tooyour kişisel sertifika deposuna aktarın ve güvenilen kök sertifika yetkilileri sertifika deposuna hello.</li>
</ul>
<br/>Merhaba üretim sertifika isteği tooyour sertifika yetkilisi gönderirken, aşağıdaki sertifika özelliklere hello verin:
<br/>

<ul>
<li><strong>Gelişmiş Anahtar Kullanımı</strong>: Azure BizTalk Services için en azından Sunucu Kimlik Doğrulaması gerekir.</li>
<li><strong>Ortak ad</strong>: hello tam etki alanı adını (FQDN), Azure BizTalk hizmeti URL'sini girin. Bu makaledeki <a HREF="#CreateService">BizTalk Hizmeti oluşturma</a> bölümüne bakın.</li>
</ul>
<br/>
Merhaba BizTalk hizmeti oluşturulduktan sonra yeni veya farklı bir sertifika eklenebilir.
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a>Karma Bağlantılar
Azure BizTalk hizmeti oluşturduğunuzda, hello **karma bağlantılar** sekmesi kullanılabilir:

![Karma Bağlantılar Sekmesi][HybridConnectionTab]

Karma bağlantılar olan kullanılan tooconnect bir Azure Web sitesine veya Azure mobil hizmeti tooany şirket içi SQL Server, MySQL, HTTP Web API'leri, Mobile Services ve birçok özel Web hizmeti gibi statik TCP bağlantı kullanan kaynaklara.  Karma bağlantılar ve hello BizTalk bağdaştırıcı hizmeti farklıdır. Merhaba BizTalk bağdaştırıcı hizmeti kullanılan tooconnect Azure BizTalk Services tooan şirket içi iş kolu (LOB) sistemidir.

 Bkz: [karma bağlantılar](integration-hybrid-connection-overview.md) oluşturma ve yönetme karma bağlantılar dahil olmak üzere daha fazla toolearn.

## <a name="next-steps"></a>Sonraki adımlar
Bir BizTalk hizmeti oluşturuldu, hello ile farklı öğrenmeniz [BizTalk Services: pano, İzleyici ve ölçek sekmeleri](biztalk-dashboard-monitor-scale-tabs.md). BizTalk Hizmeti uygulamalarınız için hazır. uygulamaları, Git çok oluşturma toostart[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Ayrıca bkz.
* [BizTalk Services: Sürümler Grafiği](biztalk-editions-feature-chart.md)<br/>
* [BizTalk Services: Durum Grafiği](biztalk-service-state-chart.md)<br/>
* [BizTalk Services: Yedekleme ve Geri Yükleme](biztalk-backup-restore.md)<br/>
* [BizTalk Services: Azaltma](biztalk-throttling-thresholds.md)<br/>
* [BizTalk Services: Verenin Adı ve Verenin Anahtarı](biztalk-issuer-name-issuer-key.md)<br/>
* [I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Karma Bağlantılar](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
