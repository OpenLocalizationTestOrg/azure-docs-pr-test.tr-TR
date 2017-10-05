---
title: "SharePoint Azure AD uygulama proxy'si ile uzaktan erişimi etkinleştir | Microsoft Docs"
description: "Bir şirket içi SharePoint sunucusu Azure AD uygulama proxy'si ile tümleştirme hakkında temel bilgiler yer almaktadır."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 97eeec3b3936bcbef6ac3966b890332901bcb153
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-remote-access-to-sharepoint-with-azure-ad-application-proxy"></a>SharePoint Azure AD uygulama proxy'si ile uzaktan erişimi etkinleştir

Bu makalede, Azure Active Directory (Azure AD) uygulama ara sunucusu ile bir şirket içi SharePoint sunucusu tümleştirme anlatılmaktadır.

SharePoint Azure AD uygulama proxy'si ile uzaktan erişimi etkinleştirmek için bu makaledeki adım adım bölümler izleyin.

## <a name="prerequisites"></a>Ön koşullar

Bu makalede, ortamınızda SharePoint 2013 veya daha yeni zaten sahip olduğunuzu varsayar. Ayrıca, aşağıdaki önkoşulları göz önünde bulundurun:

* SharePoint yerel Kerberos desteği içerir. Bu nedenle, iç siteleri Azure AD uygulama proxy'si aracılığıyla uzaktan erişen kullanıcılar, çoklu oturum açma (SSO) deneyimi sağlamak için kabul edilebilir.

* SharePoint server'ınızı birkaç yapılandırma değişiklikleri yapmanız gerekir. Hazırlama ortamında kullanmanızı öneririz. Bu şekilde, güncelleştirmelerinin hazırlama sunucunuza ilk olması ve üretime geçmeden önce bir test döngüsü kolaylaştırmak.

* Biz yayımlanan URL üzerinde SSL gerektirdiğinden SharePoint için SSL kurma zaten ayarladığınızdan varsayalım. SSL gönderilen ve eşlenen bağlantılar doğru olduğundan emin olmak için iç sitenizde etkin olması gerekir. SSL yapılandırmadıysanız bkz [SharePoint 2013 için SSL yapılandırma](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) yönergeler için. Ayrıca, bağlayıcı makine dağıttığınız sertifika güvendiğinden emin olun. (Sertifika herkese açık şekilde verilmesi gerekmez.)

## <a name="step-1-set-up-single-sign-on-to-sharepoint"></a>1. adım: çoklu oturum açma SharePoint'e ayarlama

Müşterilerimizin en iyi SSO deneyimi bu durumda kendi arka uç uygulamalar için SharePoint server istiyor. Yeniden kimlik doğrulaması için istenmez çünkü bu ortak Azure AD senaryoda kullanıcı yalnızca bir kez kimlik doğrulaması.

Gerektiren veya Windows kimlik doğrulaması kullanan şirket içi uygulamalar için Kerberos kimlik doğrulama protokolünü ve kısıtlı Kerberos temsilci (KCD) adlı bir özellik kullanarak SSO elde edebilirsiniz. Kullanıcı Windows doğrudan oturum kurmadı olsa bile yapılandırıldığında, KCD, bir kullanıcının windows bilet/belirteci almak uygulama ara sunucusu Bağlayıcısı sağlar. KCD hakkında daha fazla bilgi için bkz: [Kerberos Kısıtlı temsilci genel bakış](https://technet.microsoft.com/library/jj553400.aspx).

Bir SharePoint sunucusu için KCD ayarlamak için aşağıdaki sıralı bölümlerdeki yordamları kullanın:

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a>SharePoint hizmet hesabı altında çalıştığından emin olun

İlk olarak, SharePoint bir tanımlanmış hizmet hesabı altında--değil yerel sistem, yerel hizmet veya ağ hizmeti çalışır durumda olduğundan emin olun. Geçerli bir hesap için hizmet asıl adları (SPN) iliştirebilirsiniz böylece bunu yapabilirsiniz. SPN'ler Kerberos protokolü farklı hizmetleri nasıl tanımlar ' dir. Ve daha sonra KCD yapılandırmak için hesabı gerekir.

Sitelerinizi tanımlanmış hizmet hesabı altında çalıştığından emin olmak için aşağıdaki adımları gerçekleştirin:

1. Açık **SharePoint 2013 Yönetim Merkezi** site.
2. Git **güvenlik** seçip **hizmet hesaplarını yapılandır**.
3. Seçin **Web uygulama havuzu - SharePoint - 80**. Seçenekler, web havuzu adına göre biraz farklı olabilir veya web havuzu varsayılan olarak SSL kullanıyorsa.

  ![Bir hizmet hesabı yapılandırma seçenekleri](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. Varsa **bu bileşen için bir hesap seçin** olan **yerel hizmet** veya **ağ hizmeti**, bir hesap oluşturmanız gerekir. Değilse, tamamlanmış ve sonraki bölüme geçebilirsiniz.
5. Seçin **kaydı yeni yönetilen hesabı**. Hesabınızı oluşturduktan sonra ayarlamalısınız **Web uygulama havuzu** hesabını kullanabilmeniz için.

> [!NOTE]
Daha önce oluşturulmuş olmasına gerek hizmeti için Azure AD hesabı. Bir otomatik parola değişikliğini izin öneririz. Adımları ve sorunlarını giderme tamamını hakkında daha fazla bilgi için bkz: [SharePoint 2013'te Otomatik parola değişikliği yapılandırma](https://technet.microsoft.com/library/ff724280.aspx).

### <a name="configure-sharepoint-for-kerberos"></a>Kerberos için SharePoint Yapılandırma

Bu, yalnızca Kerberos ile çalışır ve çoklu oturum açma SharePoint sunucusuna gerçekleştirmek için KCD kullanın.

SharePoint siteniz için Kerberos kimlik doğrulamasını yapılandırmak için:

1. Açık **SharePoint 2013 Yönetim Merkezi** site.
2. Git **Uygulama Yönetimi**seçin **web uygulamalarını yönetme**, SharePoint sitenizi seçin. Bu örnek, **SharePoint - 80**.

  ![SharePoint sitesi seçme](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. Tıklatın **kimlik doğrulama sağlayıcıları** araç çubuğunda.
4. İçinde **kimlik doğrulama sağlayıcıları** kutusunda, **varsayılan bölge** ayarlarını görüntülemek için.
5. İçinde **Düzenle kimlik doğrulama** iletişim kutusunda, görene kadar aşağı kaydırın **talep kimlik doğrulama türleri** ve emin her ikisi de **Windows kimlik doğrulamasını etkinleştir** ve **Tümleşik Windows kimlik doğrulaması** seçilir.
6. Aşağı açılan kutusunda olduğundan emin olun **Negotiate (Kerberos)** seçilir.

  ![Kimlik doğrulama iletişim kutusunu Düzenle](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. Ekranın alt kısmındaki **kimlik doğrulamasını Düzenle** iletişim kutusu, tıklatın **kaydetmek**.

### <a name="set-a-service-principal-name-for-the-sharepoint-service-account"></a>SharePoint hizmet hesabı hizmet asıl adı ayarlama

KCD yapılandırmadan önce yapılandırdığınız hizmet hesabı olarak çalışan SharePoint hizmeti tanımlamak gerekir. Bunun için bir SPN ayarlayarak. Daha fazla bilgi için bkz: [hizmet asıl adları](https://technet.microsoft.com/library/cc961723.aspx).

SPN biçimi şöyledir:

```
<service class>/<host>:<port>
```

SPN biçimi:

* _hizmet sınıfı_ hizmeti için benzersiz bir addır. SharePoint için kullandığınız **HTTP**.

* _ana bilgisayar_ tam etki alanı ya da hizmetini çalıştıran ana bilgisayarın NetBIOS adı. Bir SharePoint sitesi için bu metni kullandığınız IIS sürümüne bağlı olarak site URL'sini olması gerekebilir.

* _bağlantı noktası_ isteğe bağlıdır.

SharePoint sunucusu FQDN'si ise:

```
sharepoint.demo.o365identity.us
```

SPN sonra:

```
HTTP/ sharepoint.demo.o365identity.us demo
```

SPN'ler belirli siteleri için sunucunuzda ayarlamak gerekebilir. Daha fazla bilgi için bkz: [yapılandırma Kerberos kimlik doğrulaması](https://technet.microsoft.com/library/cc263449(v=office.12).aspx). Kapat dikkat bölümüne "Kerberos kimlik doğrulaması kullanan Web uygulamalarınız için Create hizmet asıl adları."

SPN'ler ayarlamanızı en kolay yolu zaten siteleriniz için bulunabilecek SPN biçimleri izlemektir. Karşı hizmet hesabını kaydetmek için bu SPN kopyalayın. Bunu yapmak için:

1. SPN sitesiyle başka bir makineden göz atın.
 Bunu yaptığınızda, Kerberos biletleri ilgili kümesini makinede önbelleğe alınır. Bu biletleri için taranan hedef site SPN'sini içerir.

2. Adlı bir araç kullanarak bu site için SPN çekebilir [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html). Siteyi tarayıcıda erişen kullanıcının aynı bağlamda çalışan bir komut penceresinde aşağıdaki komutu çalıştırın:
```
Klist
```
Klist sonra hedef SPN kümesini döndürür. Bu örnekte vurgulanmış gerekli olan SPN değeridir:

  ![Örnek Klist sonuçları](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. SPN sahip olduğunuza göre bunu doğru şekilde daha önce web uygulaması için ayarladığınız hizmet hesabının yapılandırıldığından emin olmanız gerekir. Komut isteminden aşağıdaki komutu etki alanının yönetici olarak çalıştırın:

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 Bu komut olarak çalışan SharePoint hizmet hesabı SPN'yi ayarlar _demo\sp_svc_.

 Değiştir _http/sharepoint.demo.o365identity.us_ sunucunuz için SPN ile ve _demo\sp_svc_ , ortamınızdaki hizmet hesabıyla. Bunu eklemeden önce SPN'yi Setspn komut arar. Bu durumda, görebileceğiniz bir **yinelenen SPN değeri** hata. Bu hatayı görürseniz, değer hizmeti hesabı ile ilişkili olduğundan emin olun.

SPN -m seçeneğiyle Setspn komutunu çalıştırarak eklendiğini doğrulayabilirsiniz. Bu komut hakkında daha fazla bilgi için bkz: [Setspn](https://technet.microsoft.com/library/cc731241.aspx).

### <a name="ensure-that-the-connector-is-set-as-a-trusted-delegate-to-sharepoint"></a>Bağlayıcı SharePoint'e güvenilen temsilci olarak ayarlandığından emin olun

KCD, Azure AD uygulama proxy'si hizmeti kullanıcı kimlikleri SharePoint hizmetine devredebilirsiniz şekilde yapılandırın. Kullanıcılarınızın Azure AD içinde kimlik doğrulaması için Kerberos biletleri almak uygulama ara sunucusu Bağlayıcısı etkinleştirerek bunu yapabilirsiniz. Daha sonra sunucu bağlamı hedef uygulama ya da SharePoint için bu durumda geçirir.

KCD yapılandırmak için her bağlayıcı makine için aşağıdaki adımları yineleyin:

1. Bir etki alanı denetleyicisinin etki alanı yöneticisi olarak oturum açın ve ardından açın **Active Directory Kullanıcıları ve Bilgisayarları**.
2. Bağlayıcı üzerinde çalıştığı bilgisayar bulunamadı. Bu örnekte, aynı SharePoint sunucusudur.
3. Bilgisayarı çift tıklatın ve ardından **temsilci** sekmesi.
4. Temsilci ayarları ayarlandığından emin olun **bu bilgisayara yalnızca belirtilen hizmetlere temsilci seçmek için güven**ve ardından **herhangi bir kimlik doğrulama protokolünü kullan**.

  ![Temsilci ayarları](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. Tıklatın **Ekle** düğmesini tıklatın, **kullanıcılar veya bilgisayarlar**ve hizmet hesabını bulun.

  ![Hizmet hesabı için SPN ekleme](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. SPN'ler listesinde, hizmet hesabı için daha önce oluşturduğunuz bir tanesini seçin.
7. **Tamam** düğmesine tıklayın. Tıklatın **Tamam** yeniden değişiklikleri kaydedin.

## <a name="step-2-enable-remote-access-to-sharepoint"></a>2. adım: SharePoint için uzaktan erişimi etkinleştir

Kerberos ve yapılandırılmış KCD için SharePoint etkinleştirdikten, çoklu oturum açma SharePoint'e ayarlamak hazırsınız. Ardından bir bağlayıcı, SharePoint grubu Azure AD uygulama proxy'si aracılığıyla uzaktan erişim için yayımlayabilirsiniz.

Aşağıdaki adımları gerçekleştirmek için kuruluşunuzun Azure Active Directory hesabında genel yönetici rolünün bir üyesi olmanız gerekir.

1. Oturum [Azure portal](https://manage.windowsazure.com) ve Azure AD kiracınıza bulabilirsiniz.
2. Tıklatın **uygulamaları**ve ardından **Ekle**.
3. **Publish an application that will be accessible from outside your network (Ağınızın dışından erişilebilecek olan bir uygulamayı yayımlama)** seçeneğini belirleyin. Bu seçeneği görmüyorsanız, Azure AD temel sahip veya Kiracı Premium ayarlanan emin olun.
4. Seçeneklerin her biri aşağıdaki gibi tamamlayın:
 * **Ad**:--Örneğin, istediğiniz herhangi bir değer kullanmak **SharePoint**.
 * **İç URL**: SharePoint site URL'sidir dahili olarak gibi **https://SharePoint/**. Bu örnekte, kullandığınızdan emin olun **https**.
 * **Ön kimlik doğrulama yöntemi**: seçin **Azure Active Directory**.

  ![Bir uygulama eklemek için Seçenekler](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. Uygulama yayımlandıktan sonra tıklatın **yapılandırma** sekmesi.
6. Seçeneğine kaydırın **üstbilgileri Çevir URL'de**. Varsayılan değer **Evet**. Şekilde değiştirin **Hayır**.

 SharePoint kullanan _ana bilgisayar üstbilgisi_ siteyi aramak için değer. Aynı zamanda bu değere göre bağlantılar da oluşturur. Net etkisi, SharePoint oluşturur herhangi bir bağlantıyı dış URL'yi kullanmak üzere doğru şekilde ayarlanmış bir yayımlanan URL olduğundan emin olmaktır. Ayar değeri **Evet** Ayrıca arka uç uygulama isteği iletmek bağlayıcı sağlar. Ancak, ayar değeri **Hayır** bağlayıcı iç ana bilgisayar adını göndermez anlamına gelir. Bunun yerine, ana bilgisayar üstbilgisi bağlayıcı arka uç uygulaması için yayımlanan URL olarak gönderir.

 Ayrıca, SharePoint bu URL'yi kabul etmesini sağlamak için SharePoint sunucusu üzerindeki bir daha fazla yapılandırmayı tamamlamak gerekir. Bu sonraki bölümde gerçekleştirirsiniz.

7. Değişiklik **iç kimlik doğrulama yöntemini** için **tümleşik Windows kimlik doğrulaması**. Azure AD kiracınıza UPN şirket içinden farklı bulutta UPN kullanıyorsa, güncelleştirmeyi unutmayın **oturum açma kimlik temsilcisi** de.
8. Ayarlama **iç uygulama SPN** daha önce belirlediğiniz değeri. Örneğin, **http/sharepoint.demo.o365identity.us**.
9. Hedef kullanıcılarınızın uygulamaya atayın.

Uygulamanızı aşağıdaki örneğe benzer görünmelidir:

  ![Tamamlanan uygulama](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-the-external-url"></a>Adım 3: SharePoint dış URL hakkında bilir emin olun.

Böylece, dış URL temel alınarak bağlantılar kılacak SharePoint dış URL temel alınarak site bulabilirsiniz emin olmak için son adımı. Bunun için SharePoint sitesi için diğer erişim eşleşmeleri yapılandırarak.

1. Açık **SharePoint 2013 Yönetim Merkezi** site.
2. Altında **sistem ayarlarını**seçin **yapılandırma diğer erişim eşleşmeleri**.

 Bu açılır **diğer erişim eşleşmeleri** kutusu.

  ![Diğer erişim eşleşmeleri kutusu](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. Aşağı açılan listesinde **alternatif erişim eşleme koleksiyonu**seçin **değişiklik alternatif erişim eşleme koleksiyonu**.
4. Örneğin, siteniz--seçin **SharePoint - 80**.

  ![Bir site seçme](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. Bir iç URL veya genel bir URL olarak yayımlanan URL'ye eklemeyi seçebilirsiniz. Bu örnek genel bir URL extranet kullanır.
6. ' I tıklatın **Düzenle ortak URL'leri** içinde **Extranet** yolu, önceki adımda olduğu gibi yayımlanan uygulama için yolunu girin. Örneğin **https://sharepoint-iddemo.msappproxy.net**.

  ![Yolun girme](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. **Kaydet** düğmesine tıklayın.

 Artık Azure AD uygulama proxy'si aracılığıyla harici olarak SharePoint sitesine erişebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

- [Şirket içi uygulamalara güvenli uzaktan erişim sağlama](active-directory-application-proxy-get-started.md)
- [Azure AD uygulama proxy'si bağlayıcılar anlama](application-proxy-understand-connectors.md)
- [SharePoint 2016 ve Office Online Server Azure AD uygulama proxy'si ile uygulama yayımlama](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
