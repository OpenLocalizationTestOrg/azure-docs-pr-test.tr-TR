---
title: "Uygulama proxy'si uygulama toouse Kerberos Kısıtlı temsilci aaaHow tooconfigure | Microsoft Docs"
description: "Nasıl bir Azure AD uygulama proxy'si uygulama için Kerberos Kısıtlı temsilci tooconfigure."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 93dac264ff1d3b99dead1d9c759c37c59373cbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-kerberos-constrained-delegation"></a>Nasıl tooconfigure uygulama proxy'si uygulama toouse Kerberos Kısıtlı temsilci

Merhaba uygulamaları uygulama tooapplication ve Azure uygulama proxy'si hello kutusu dışında sağ sunar hello seçeneklerden birini biraz değişebilir SSO toopublished elde etmek için kullanılabilen yöntemler olan Kerberos Kısıtlı temsilci (KCD). Bir bağlayıcı konak yapılandırılmış tooperform kısıtlı kerberos kimlik doğrulaması toobackend uygulamalar, kullanıcılar adına olduğu budur.

KCD etkinleştirmek için gerçek yordam hello oldukça basittir ve genellikle hello genel bir anlayış en çok çeşitli bileşenler ve SSO kolaylaştıran kimlik doğrulaması akışı gerektirir. Bilgi toohelp iyi kaynaklarının nerede KCD SSO beklendiği gibi işlev olmayan senaryolar sorun giderme bulma, seyrek olabilir.

Bu nedenle, bu makalede tooprovide tek bir sorun giderme ve bazı biz bkz hello en yaygın sorunları otomatik olarak düzeltmek yardımcı olması başvuru noktası çalışır. Merhaba tanılamak için aynı süre teklif ek yönergeler daha karmaşık hello ve uyarlamasını troubled.

Bu makalede varsayımlar aşağıdaki hello kullandığına dikkat edin:

-   Azure uygulama proxy'si dağıtılan göre bizim [belgelerine](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable) ve genel erişim toonon KCD uygulamaları beklendiği gibi çalıştığını.

-   Merhaba yayımlanan hedef uygulama IIS ve Microsoft'un kerberos üzerinde temel alır.

-   Merhaba sunucu ve uygulama ana bilgisayar tek bir Active Directory etki alanında bulunur. Etki alanı ve orman senaryoları çapraz ilgili ayrıntılı bilgiler bulunabilir bizim [KCD Teknik İnceleme](http://aka.ms/KCDPaper).

-   Merhaba konu uygulama yayımlanan bir Azure Kiracı ile ön kimlik doğrulama etkinleştirildi ve kullanıcıların tooauthenticate tooAzure aracılığıyla forms tabanlı kimlik doğrulama beklenir. Zengin istemci kimlik doğrulama senaryoları bu makalenin kapsamında değildir, ancak gelecekteki hello belirli bir noktada eklenmesi.

## <a name="prerequisites"></a>Ön koşullar

Azure uygulama Proxy altyapısını neredeyse herhangi bir tür dağıtılabilir veya ortam ve hello mimarileri Şüphesiz kuruluş tooorganization farklı. Merhaba en yaygın nedenlerinden biri KCD sorunları hello ortamları kendileri ancak bunun yerine basit yanlış yapılandırmaları veya genel gözetim değil ilişkilidir.

Bu nedenle, bizim öneriler her zaman toostart bizim ana düzenlendiği tüm hello ön koşul karşılanır olduğundan emin olarak tarafından [KCD SSO'su kullanarak hello uygulama proxy'si makale](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) önce başlatma sorunlarını giderme.

Bu önceki sürümlerinde Windows, aynı zamanda bazı başka noktalar oluşturduğunu sırasında temelde farklı bir yaklaşım tooconfiguring KCD kullanır gibi KCD 2012R2 üzerinde yapılandırma konusunda özellikle hello bölümü:

-   Bir etki alanı üye sunucusu tooopen belirli etki alanı denetleyicisiyle güvenli kanal iletişim için seyrek değil. Bağlayıcı konakları genellikle yalnızca belirli yerel site DC'leri ile kısıtlı toobeing mümkün toocommunicate olmamalıdır şekilde tooanother iletişim belirli bir zamanda taşıyın.

-   Benzer toohello noktası yukarıdaki etki alanları arası senaryolar hello yerel ağ çevre dışında yer alabileceği bir bağlayıcı konak tooDCs doğrudan başvuruları kullanır. Eşit olduğu Bu senaryoda önemli toomake başlayarak trafiği diğer ilgili etki alanları, aksi takdirde temsilci temsil eden tooDCs de izin emin başarısız.

-   Bunlar bazen zorlayıcı ve çekirdek RPC trafiğine engel olarak mümkün olduğunda, tüm etkin IP'leri/Kimlikler cihazlar bağlayıcı konakları ve DC'leri arasında yerleştirmekten kaçınmalısınız

Tooresolve sorunları hızla isteriz ve etkili bir şekilde zaman alabilir kadar bu nedenle, mümkün olduğunda deneyin ve gerekir hello senaryoları basit temsilci test. Daha fazla değişken, tanıtmak Merhaba, hello daha, toocontend sahip olabilir. Örneğin, test tooa tek Bağlayıcınızı sınırlama değerli zamandan tasarruf edebilirsiniz ve hello sorunları giderildikten sonra ek bağlayıcı eklenebilir.

Olası çalışırsanız ve test etmek için hello mimarisi tooa tam minimum en aza bazı çevresel etmenler de tooan sorun, böylece yeniden katkıda bulunan. Örneğin, yanlış yapılandırılmış iç güvenlik duvarı ACL'ler seyrek, böylece mümkünse düz toohello DC'leri ve arka uç uygulaması aracılığıyla izin verilen bir bağlayıcı gelen tüm trafiği vardır. 

Gerçekte hello mutlak en iyi yeri tooposition bağlayıcılar olabilir yakın tootheir hedefleri olur. Bir Güvenlik Duvarı'nı sat satır içi sahip yalnızca sınama adımında gereksiz karmaşıklık ekler ve yalnızca, araştırmalar uzatmak.

Bu nedenle, nelerin KCD sorun yine de oluşturduğunu? İyi var. KCD bir sorun başarısız olan ve hello ilk belirtileri genellikle kendileri de bildirim SSO birkaç Klasik göstergeleri tarayıcı hello.

   ![Yanlış KCD yapılandırma hatası](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic1.png)

   ![Yetkilendirme toomissing izinleri başarısız oldu](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic2.png)

hangi tooperform SSO başarısız ve sonuç olarak reddetme aynı belirti ayı hello tüm kullanıcı erişimi toohello uygulaması hello.

## <a name="troubleshooting"></a>Sorun giderme

Ardından sorun giderme nasıl hello sorunu ve gözlemlenen Belirtiler bağlıdır. Henüz gelmiş olabilir üzerinden değil yararlı bilgiler içerdiğinden herhangi geçmeden önce daha fazla bağlantılar, aşağıdaki hello önerdiğimiz:

-   [Uygulama proxy'si sorunları ve hata iletileri sorunlarını giderme](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot)

-   [Kerberos hataları ve belirtileri](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#kerberos-errors)

-   [SSO ile çalışan, şirket içi ve bulut kimlikleri aynı değildir](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd#working-with-sso-when-on-premises-and-cloud-identities-are-not-identical)

Sorun, bu kadar ardından hello ana becerilere sahipseniz kesinlikle bulunmaktadır. Toodig daha derin, gereksinim duyduğunuz giderebileceğinizi üç ayrı aşamaları hello akışına ayırarak başlatın.

**İstemcisi ön kimlik doğrulaması** -hello dış kullanıcı tooAzure bir tarayıcı aracılığıyla kimlik doğrulaması.

Mümkün toopre edilen-kimlik doğrulaması tooAzure KCD SSO toofunction kesinlik temelli. Bu test edilip herhangi bir sorun varsa, ilk olarak ele. Merhaba ön kimlik doğrulama aşama hiçbir ilişkisi tooKCD veya hello sahip olduğuna dikkat edin, uygulama yayımlanır. Bu oldukça kolay toocorrect uyumsuzlukları sağlamlık hello konu hesabı denetimi tarafından Azure'da var olmalıdır ve, olmadığını devre dışı bırakılmış/engelledi. Merhaba hata yanıtı hello tarayıcıda genellikle açıklayıcı yeterince toounderstand hello neden olabilir. Emin değilseniz, diğer sorun giderme belgeleri tooverify kontrol edebilirsiniz.

**Temsilci hizmet** -kullanıcılar adına bir kerberos hizmet biletini bir KDC (Kerberos Dağıtım Merkezi), alma Azure Ara sunucusu Bağlayıcısı hello.

Merhaba dış iletişimleri hello istemci hello Azure ön uç arasında şifrelemeyle KCD üzerinde doğabilecek, diğerinden sağlama çalıştığını olması gerekir. Böylece Hello Azure Proxy Hizmeti kullanılan tooobtain bir kerberos anahtarı olması geçerli bir kullanıcı kimliği ile sağlanan budur. Bu KCD mümkün değildir ve başarısız olacağı olmadan.

Daha önce belirtildiği gibi hello tarayıcı hata iletileri şey neden başarısız iyi bazı ipuçları genellikle sağlar. Bu izin, toocorrelate hello davranışı tooactual olayları hello Azure Proxy olay günlüğü'nde hello etkinlik kimliği ve zaman damgası aşağı emin toonote hello yanıtta kılın.

   ![Yanlış KCD yapılandırma hatası](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic3.png)

Ve hello karşılık gelen girişleri görülen hello olay günlüğü olay 13019 veya 12027 görülen. Bağlayıcı olay günlüklerinde hello bulabilirsiniz **uygulama ve hizmet günlükleri** &gt; **Microsoft** &gt; **AadApplicationProxy** &gt; **Bağlayıcı**&gt;**yönetici**.

   ![Uygulama proxy'si olay günlüğündeki olay 13019](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic4.png)

   ![Uygulama proxy'si olay günlüğündeki olay 12027](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic5.png)

-   Bir A kaydı iç DNS sunucunuzun hello uygulamanın adresi ve bir CName kullanın

-   Merhaba bağlayıcı barındıran hedef hesabının SPN ve atanan hello hakları toodelegate toohello verildiğini yeniden onaylayın **herhangi bir kimlik doğrulama protokolünü kullan** seçilir. Bu bizim ana kapsamdaki [SSO yapılandırma makale](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)

-   Olduğunu hello SPN varlığı AD içinde yalnızca tek bir örneğini vererek doğrulayın bir **setspn - x** herhangi bir etki alanı üye ana bir komut isteminden

-   Bir etki alanı ilkesi yaşanıyorsa toosee zorlanan toolimit hello denetleyin [en büyük boyut verilen kerberos belirteçlerin](https://blogs.technet.microsoft.com/askds/2012/09/12/maxtokensize-and-windows-8-and-windows-server-2012/)gibi bir belirteç edinme öğesinden bu engelle hello bağlayıcı toobe aşırı bulundu

Merhaba alışverişleri hello bağlayıcı konağı ve etki alanı KDC arasında yakalama bir ağ izlemesi sonra daha düşük düzey ayrıntı hello sorunları alma hello sonraki en iyi adım olacaktır. Bu konuda bulabilirsiniz [derinlemesine sorun giderme kağıt](https://aka.ms/proxytshootpaper).

Raporlama iyi görünüyorsa, bir olay bir 401 döndürme toohello uygulama kimlik doğrulamasının başarısız belirten hello günlüklerine görmeniz gerekir. Bu genellikle, bilet reddetme bu hello hedef uygulama gösterir, böylece sonraki aşamaya aşağıdaki hello ile devam.

**Hedef uygulama** -hello Bağlayıcısı tarafından sağlanan hello kerberos bileti hello tüketicisi

Bu aşama hello bağlayıcı sırasında beklenen toohave bir kerberos hizmet bileti toohello arka üstbilgisi hello ilk uygulama isteği içinde olarak gönderilir.

-   Merhaba uygulamanın kullanarak hello Portalı'nda tanımlanan iç URL'yi doğrula Merhaba uygulaması hello bağlayıcı konaktaki hello tarayıcısından doğrudan erişilebilir olduğunu. Ardından, başarılı bir şekilde oturum açabilirsiniz. Bunun yapılması ile ilgili ayrıntılar hello connector sorunlarını giderme sayfasında bulunabilir.

-   Merhaba tarayıcı arasındaki bu hello kimlik doğrulaması hala hello bağlayıcı konakta onaylayın ve Merhaba uygulaması, kerberos, hello aşağıdakilerden birini yaparak kullanıyor:

1.  Geliştirme araçları çalıştırma (**F12**) Internet Explorer ya da kullanım [Fiddler](https://blogs.msdn.microsoft.com/crminthefield/2012/10/10/using-fiddler-to-check-for-kerberos-auth/) hello bağlayıcı ana bilgisayardan. Merhaba iç URL'yi kullanarak toohello uygulamasına gidin ve hello uygulamasından hello yanıtta döndürülen WWW yetkilendirme üstbilgileri sunulan hello inceleyin, ya da anlaşma tooensure veya kerberos mevcuttur. Bir sonraki kerberos blob hello yanıtta döndürülen hello tarayıcı toohello genellikle uygulama başlayarak **YII**bu göstergesidir oynama olan kerberos gelir. NTLM hello üzerinde her zaman diğer yandan başlayarak **TlRMTVNTUAAB**, Base64 kodlaması kodunu çözdü zaman NTLMSSP okur. Görürseniz **TlRMTVNTUAAB** hello blob hello başlangıcında, bu Kerberos anlamına gelir **değil** kullanılabilir. Bu görmüyorsanız, Kerberos olasıdır kullanılabilir.

  * Not: Fiddler, kullanıyorsanız bu yöntem geçici olarak hello uygulamanın yapılandırma dosyasında IIS üzerinde genişletilmiş koruma devre dışı bırakılması gerekir.

     ![Ağ İnceleme tarayıcının](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic6.png)

    *Şekil:* TIRMTVNTUAAB ile başlamıyor olduğundan, bu Kerberos kullanılabilir bir örnektir. Bu, YII ile başlamıyor Kerberos Blob örneğidir.

2.  Geçici olarak NTLM IIS site ve erişim uygulamasından doğrudan IE bağlayıcı konaktaki üzerinde hello sağlayıcıları listesinden kaldırın. Merhaba sağlayıcılar listesinde artık NTLM ile mümkün tooaccess Merhaba uygulaması yalnızca Kerberos kullanılarak olmalıdır. Bu başarısız olursa, daha sonra hello uygulamanın yapılandırma ile ilgili bir sorun yoktur ve Kerberos kimlik doğrulaması çalışmıyor önerir.

Kerberos kullanılabilir durumda değilse, IIS toomake emin ayarlarında anlaşma onay hello uygulamanın kimlik doğrulaması en üstteki hemen altındaki NTLM ile listelenir. (Değil Anlaş: kerberos veya anlaşma: pku2u ile). Yalnızca Kerberos işlevsel ise devam edin.

   ![Windows kimlik doğrulama sağlayıcıları](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic7.png)
   
-   Kerberos ve NTLM yerinde ile Merhaba portalında hello uygulaması için ön kimlik doğrulaması şimdi geçici olarak devre dışı olanak sağlar. Hello erişebildiğinizi varsa bkz hello dış URL'yi kullanarak Internet. İstendiğinde tooauthenticate olmalıdır ve hello ile kullanılan hello aynı hesap adına mümkün toodo olmalıdır önceki adımı. Aksi durumda, bu hiç Merhaba arka uç uygulaması ve değil KCD bir sorun gösterir.

-   Şimdi hello Portalı'nda ön kimlik doğrulama yeniden etkinleştirin ve tooconnect toohello uygulaması, dış URL yoluyla deneyerek Azure üzerinden kimlik doğrulaması. SSO başarısız olursa, hello tarayıcı yanı sıra 13022 olay günlüğünde olay hello Yasak hata iletisini görmeniz gerekir:

    *Microsoft AAD Application Proxy Connector, çünkü bir HTTP 401 hata ile tooKerberos kimlik doğrulama girişimlerini Hello arka uç sunucusuna yanıtlar hello kullanıcının kimliğini doğrulayamıyor.*

    ![HTTTP 401 Yasak hata alır](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic8.png)

-   SPN hello aynı hesabı karşı AD içinde aşağıda gösterildiği gibi IIS'de giderek yapılandırıldı yapılandırılmış toouse hello Hello IIS uygulama tooensure yapılandırılmış hello uygulama havuzu denetleyin

    ![IIS uygulama yapılandırma penceresi](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic9.png)

    Merhaba kimlik öğrendikten sonra bu hesabı kesinlikle SPN söz konusu hello ile yapılandırıldığından emin bir cmd komut istemi toomake hello aşağıdakini gönderin. Örneğin, **setspn – q http/spn.wacketywack.com**

    ![SetSPN komut penceresi](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic10.png)

-   Merhaba portalındaki hello uygulamanın ayarları karşı tanımlanmış SPN hello hedef AD hesabı hello uygulamanın uygulama havuzunun kullandığı karşı yapılandırılmış aynı SPN hello bu hello denetleyin

   ![Azure Portalı'nda SPN yapılandırma](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic11.png)
   
-   IIS ve select hello na **yapılandırma Düzenleyicisi** seçeneği hello uygulama için ve çok gidin**system.webServer/security/authentication/windowsAuthentication** toomake emin bu **UseAppPoolCredentials** tootrue ayarlayın

   ![IIS yapılandırması uygulama havuzları seçeneği kimlik bilgisi](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic12.png)

Yararlı Kerberos işlemlerinin Hello performansını geliştirmeye devam ederken, çekirdek modu etkin bırakarak ayrıca hello hello biletini neden olan makine hesabı kullanarak şifresi hizmet toobe istedi. Bu nedenle bu kümesi tootrue sonu sahip hello yerel sistem olarak da adlandırılır Merhaba uygulaması bir grupta birden fazla sunucuda barındırılıyorsa KCD.

-   Ek bir onay toodisable hello ayrıca isteyebilir **Genişletilmiş** koruma çok. Bir uygulama hello varsayılan Web sitesi bir alt klasörü burada yayımlanan burada bu toobreak belirli yapılandırmalarında etkinleştirildiğinde KCD oluyor uygulamasına yol açıyordu karşılaşılan senaryoları olmuştur. Bu kendisine bağımlı nesneler herhangi bir etkin ayarı devralarak öneren çıkışı gri hello tüm iletişim kutularını bırakarak anonim kimlik doğrulaması için yalnızca yapılandırılır. Ancak burada olası her zaman bu etkinleştirildiğinde sahip öneririz böylece her şekilde test, toorestore bu tooenabled unutmayın.

Bu ek denetimleri kullanarak, yayımlanan uygulama izleme toostart üzerinde yerleştirdiğiniz. Devam edin ve ayrıca ek bağlayıcı yukarı döndürme toodelegate yapılandırılmış, ancak sonra şeyleri daha fazla olup olmadığını biz bizim daha ayrıntılı teknik kılavuz okuma önerebileceğiniz [sorun giderme Azure AD uygulaması için hello tam Kılavuzu Proxy](https://aka.ms/proxytshootpaper)

Kullanıcısıysanız sorununuzu oluşturulamıyor tooprogress hala, destek ve mutluluk tooassist'dan çok olmalıdır buradan devam. Merhaba portalındaki doğrudan bir destek bileti oluşturun ve bizim mühendisleri tooyou ulaşabileceği.

## <a name="other-scenarios"></a>Diğer senaryolar

-   Azure uygulama proxy'si, istek tooan uygulama göndermeden önce bir Kerberos anahtarı ister. Tableau Server gibi bazı 3 taraf uygulamalar kimlik doğrulama yöntemi gibi değil ve hello yerine daha geleneksel bekliyor anlaşmaları tootake yerleştir. Merhaba ilk istek anonim bir 401 destekleyen hello kimlik doğrulama türleri ile Merhaba uygulama toorespond izin verme.

-   Burada bir uygulama, bir arka uç hem ön uç SQL Reporting Services gibi gerektiren her iki kimlik doğrulama ile katmanlı senaryolarda yaygın olarak kullanılan çift atlama kimlik doğrulaması -.

## <a name="next-steps"></a>Sonraki adımlar
[Yönetilen bir etki alanında kerberos Kısıtlı temsilci (KCD) yapılandırma](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-enable-kcd)
