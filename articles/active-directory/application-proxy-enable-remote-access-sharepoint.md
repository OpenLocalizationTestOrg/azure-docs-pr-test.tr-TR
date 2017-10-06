---
title: "Azure AD uygulama proxy'si ile aaaEnable uzaktan erişim tooSharePoint | Microsoft Docs"
description: "Merhaba ile nasıl ilgili temel bilgileri kapsayan toointegrate Azure AD uygulama proxy'si ile bir şirket içi SharePoint server."
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
ms.openlocfilehash: 6ab413462fcaf387e150449df9c97505c4108bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-access-toosharepoint-with-azure-ad-application-proxy"></a>Azure AD uygulama proxy'si ile uzaktan erişim tooSharePoint etkinleştir

Bu makalede ele nasıl toointegrate Azure Active Directory (Azure AD) uygulama ara sunucusu ile bir şirket içi SharePoint server.

Azure AD uygulama proxy'si ile tooenable uzaktan erişim tooSharePoint bu makalede adım adım hello bölümlerde izleyin.

## <a name="prerequisites"></a>Ön koşullar

Bu makalede, ortamınızda SharePoint 2013 veya daha yeni zaten sahip olduğunuzu varsayar. Ayrıca, aşağıdaki önkoşullar hello göz önünde bulundurun:

* SharePoint yerel Kerberos desteği içerir. Bu nedenle, iç siteleri Azure AD uygulama proxy'si aracılığıyla uzaktan erişen kullanıcılar bir tek oturum açma (SSO) deneyimi toohave varsayabilirsiniz.

* Toomake birkaç yapılandırma değişiklikleri tooyour SharePoint sunucusu gerekir. Hazırlama ortamında kullanmanızı öneririz. Bu şekilde, sunucu ilk hazırlama güncelleştirmeleri tooyour olun ve sonra üretime geçmeden önce bir test döngüsü kolaylaştırmak.

* URL hello SSL yayımlanan gerektirdiği için SharePoint için SSL kurma zaten ayarladığınızdan varsayalım. SSL etkin toohave bağlantılar gönderilen/doğru eşleştirildiğini olduğunu tooensure, iç sitenizin gerekir. SSL yapılandırmadıysanız bkz [SharePoint 2013 için SSL yapılandırma](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) yönergeler için. Ayrıca, dağıttığınız bu hello bağlayıcı makine güvenleri hello sertifika emin olun. (genel olarak verilen toobe hello sertifika gerekmez.)

## <a name="step-1-set-up-single-sign-on-toosharepoint"></a>1. adım: Tek oturum açma tooSharePoint ayarlama

Müşterilerimizin en iyi SSO bir deneyim arka uç için kendi uygulamalarında, SharePoint sunucu bu durumda hello istiyor. Yeniden kimlik doğrulaması için istenmez çünkü bu ortak Azure AD senaryoda hello kullanıcı yalnızca bir kez kimlik doğrulaması.

Gerektiren veya Windows kimlik doğrulaması kullanan şirket içi uygulamalar için SSO hello Kerberos kimlik doğrulama protokolünü ve kısıtlı Kerberos temsilci (KCD) adlı bir özellik kullanarak elde edebilirsiniz. Yapılandırıldığında, KCD, bir windows hello uygulama Proxy Bağlayıcısı tooobtain sağlayan hello kullanıcı tooWindows içinde doğrudan oturum kurmadı olsa bile bilet/belirtecin bir kullanıcı için. KCD, hakkında daha fazla toolearn bkz [Kerberos Kısıtlı temsilci genel bakış](https://technet.microsoft.com/library/jj553400.aspx).

bir SharePoint sunucusu için kullanım hello hello sıralı bölümleri aşağıdaki yordamlarda tooset KCD Yukarı:

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a>SharePoint hizmet hesabı altında çalıştığından emin olun

İlk olarak, SharePoint bir tanımlanmış hizmet hesabı altında--değil yerel sistem, yerel hizmet veya ağ hizmeti çalışır durumda olduğundan emin olun. Hizmet asıl adları (SPN) tooa geçerli hesabı iliştirebilirsiniz böylece bunu yapabilirsiniz. SPN'ler nasıl hello Kerberos protokolü farklı hizmetleri tanımlar ' dir. Ve hesap hello sonraki tooconfigure hello KCD.

sitelerinizin tanımlanmış hizmet hesabı altında çalışan tooensure hello aşağıdaki adımları gerçekleştirin:

1. Açık hello **SharePoint 2013 Yönetim Merkezi** site.
2. Çok Git**güvenlik** seçip **hizmet hesaplarını yapılandır**.
3. Seçin **Web uygulama havuzu - SharePoint - 80**. Merhaba web havuzu SSL varsayılan olarak kullanıyorsa veya Hello seçenekleri hello web havuzu adına göre biraz farklı olabilir.

  ![Bir hizmet hesabı yapılandırma seçenekleri](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. Varsa **bu bileşen için bir hesap seçin** olan **yerel hizmet** veya **ağ hizmeti**, toocreate bir hesap gerekir. Değilse, tamamlanmış ve toohello sonraki bölüme geçebilirsiniz.
5. Seçin **kaydı yeni yönetilen hesabı**. Hesabınızı oluşturduktan sonra ayarlamalısınız **Web uygulama havuzu** hello hesabını kullanabilmeniz için.

> [!NOTE]
Daha önce bir toohave ihtiyacınız hello hizmeti için Azure AD hesabı oluşturuldu. Bir otomatik parola değişikliğini izin öneririz. Adımları ve sorunlarını giderme hello tam kümesi hakkında daha fazla bilgi için bkz: [SharePoint 2013'te Otomatik parola değişikliği yapılandırma](https://technet.microsoft.com/library/ff724280.aspx).

### <a name="configure-sharepoint-for-kerberos"></a>Kerberos için SharePoint Yapılandırma

KCD tooperform tek oturum açma toohello SharePoint server kullanın ve bu, yalnızca Kerberos ile çalışır.

SharePoint sitesi için Kerberos kimlik doğrulamasını tooconfigure:

1. Açık hello **SharePoint 2013 Yönetim Merkezi** site.
2. Çok Git**Uygulama Yönetimi**seçin **web uygulamalarını yönetme**, SharePoint sitenizi seçin. Bu örnek, **SharePoint - 80**.

  ![Merhaba SharePoint sitesi seçme](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. Tıklatın **kimlik doğrulama sağlayıcıları** hello araç.
4. Merhaba, **kimlik doğrulama sağlayıcıları** kutusunda, **varsayılan bölge** tooview hello ayarları.
5. Merhaba, **kimlik doğrulamasını Düzenle** iletişim kutusunda, görene kadar aşağı kaydırın **talep kimlik doğrulama türleri** ve emin olun her ikisi de **Windows kimlik doğrulamasını etkinleştir** ve ** Tümleşik Windows kimlik doğrulaması** seçilir.
6. Merhaba açılan kutusunda olduğundan emin olun **Negotiate (Kerberos)** seçilir.

  ![Kimlik doğrulama iletişim kutusunu Düzenle](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. Merhaba hello sonundaki **kimlik doğrulamasını Düzenle** iletişim kutusu, tıklatın **kaydetmek**.

### <a name="set-a-service-principal-name-for-hello-sharepoint-service-account"></a>Merhaba SharePoint hizmet hesabı için bir hizmet asıl adını ayarlayın

Merhaba KCD yapılandırmadan önce yapılandırdığınız hello hizmet hesabı olarak çalışan tooidentify hello SharePoint hizmeti gerekir. Bunun için bir SPN ayarlayarak. Daha fazla bilgi için bkz: [hizmet asıl adları](https://technet.microsoft.com/library/cc961723.aspx).

Merhaba SPN biçimi şöyledir:

```
<service class>/<host>:<port>
```

Merhaba SPN biçimde:

* _hizmet sınıfı_ hello hizmeti için benzersiz bir addır. SharePoint için kullandığınız **HTTP**.

* _ana bilgisayar_ hello tam etki alanı veya hizmet hello hello ana bilgisayarın NetBIOS adını çalışıyor. Bir SharePoint sitesi için bu metni toobe hello kullanmakta olduğunuz IIS hello sürümüne bağlı olarak hello site URL'sini gerekebilir.

* _bağlantı noktası_ isteğe bağlıdır.

Merhaba hello SharePoint sunucusunun FQDN'si ise:

```
sharepoint.demo.o365identity.us
```

Merhaba SPN ise:

```
HTTP/ sharepoint.demo.o365identity.us demo
```

Ayrıca, belirli siteler için sunucunuzda tooset SPN'ler gerekebilir. Daha fazla bilgi için bkz: [yapılandırma Kerberos kimlik doğrulaması](https://technet.microsoft.com/library/cc263449(v=office.12).aspx). Kapat dikkat toohello bölüm ödeme "Kerberos kimlik doğrulaması kullanan Web uygulamalarınız için Create hizmet asıl adları."

Merhaba kolay SPN'ler tooset için zaten siteleriniz için bulunabilecek toofollow hello SPN biçimleri yoludur. Bu SPN'ler tooregister hello hizmet hesabı karşı kopyalayın. toodo bu:

1. Başka bir makineden hello SPN toohello sitesiyle göz atın.
 Merhaba olduğunda Kerberos biletleri ilgili kümesi hello makinede önbelleğe alınır. Bu biletler hello için taranan hello hedef site SPN'sini içerir.

2. Adlı bir araç kullanarak bu site için SPN hello çekebilir [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html). Hello çalışan bir komut penceresinde hello tarayıcıda erişilen hello siteyi çalıştırın hello kullanıcısı olarak aynı bağlam hello komutu aşağıdaki:
```
Klist
```
Klist sonra hedef SPN hello kümesini döndürür. Bu örnekte vurgulanmış hello hello gerekli olan SPN değeridir:

  ![Örnek Klist sonuçları](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. Merhaba SPN sahip olduğunuza göre bunu doğru şekilde önceki hello web uygulaması için ayarladığınız hello hizmet hesabının yapılandırıldığından emin toomake gerekir. Komut hello komut isteminden hello etki alanının yönetici olarak aşağıdaki hello çalıştırın:

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 Ayarlar hello SPN hello SharePoint hizmeti için bu komutu hesabı olarak çalışan _demo\sp_svc_.

 Değiştir _http/sharepoint.demo.o365identity.us_ hello SPN sunucunuz için sahip ve _demo\sp_svc_ ortamınızdaki hello hizmet hesabıyla. Bunu eklemeden önce hello Setspn komut Merhaba SPN arar. Bu durumda, görebileceğiniz bir **yinelenen SPN değeri** hata. Bu hatayı görürseniz, hello değeri hello hizmeti hesabı ile ilişkili olduğundan emin olun.

SPN hello -m seçeneğiyle hello Setspn komutunu çalıştırarak eklendi bu hello doğrulayabilirsiniz. Bu komut hakkında daha fazla toolearn bkz [Setspn](https://technet.microsoft.com/library/cc731241.aspx).

### <a name="ensure-that-hello-connector-is-set-as-a-trusted-delegate-toosharepoint"></a>Bu hello bağlayıcı güvenilen temsilci tooSharePoint ayarlandığından emin olun

Merhaba KCD Hello Azure AD uygulama proxy'si hizmeti kullanıcı kimlikleri toohello SharePoint hizmeti temsilci seçebilirsiniz şekilde yapılandırın. Merhaba uygulama ara sunucusu Bağlayıcısı etkinleştirerek tooretrieve Kerberos biletleri için Azure AD içinde kimlik doğrulaması, kullanıcılar bunu. Daha sonra sunucu hello bağlam toohello hedef uygulama ya da SharePoint bu durumda geçirir.

tooconfigure hello KCD, aşağıdaki adımları her bağlayıcı makine yineleme hello:

1. Bir etki alanı yönetici tooa DC oturum açın ve ardından açın **Active Directory Kullanıcıları ve Bilgisayarları**.
2. Bağlayıcı hello hello bilgisayarın çalışıp çalışmadığını bulun. Bu örnekte, onu sahip hello aynı SharePoint sunucusu.
3. Merhaba bilgisayarı çift tıklatın ve hello ardından **temsilci** sekmesi.
4. Merhaba temsilci ayarları çok ayarlandığından emin olun**belirtilen temsilci toohello bu bilgisayara güven yalnızca Hizmetleri**ve ardından **herhangi bir kimlik doğrulama protokolünü kullan**.

  ![Temsilci ayarları](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. Merhaba tıklatın **Ekle** düğmesini tıklatın, **kullanıcılar veya bilgisayarlar**ve hello hizmet hesabını bulun.

  ![Merhaba hizmet hesabı için SPN ekleme hello](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. SPN'ler Hello listesinde hello hello hizmet hesabı için daha önce oluşturduğunuz birini seçin.
7. **Tamam** düğmesine tıklayın. Tıklatın **Tamam** yeniden toosave hello değişiklikleri.

## <a name="step-2-enable-remote-access-toosharepoint"></a>2. adım: uzaktan erişim tooSharePoint etkinleştirme

SharePoint için Kerberos etkinleştirilmiş ve yapılandırılmış KCD göre tek oturum açma tooSharePoint yukarı hazır tooset demektir. Ardından hello bağlayıcısından hello SharePoint grubu Azure AD uygulama proxy'si aracılığıyla uzaktan erişim için yayımlayabilirsiniz.

tooperform hello adımları izleyerek toobe kuruluşunuzun Azure Active Directory hesabı hello genel yönetici rolü üyesi gerekir.

1. İçinde toohello oturum [Azure portal](https://manage.windowsazure.com) ve Azure AD kiracınıza bulabilirsiniz.
2. Tıklatın **uygulamaları**ve ardından **Ekle**.
3. **Publish an application that will be accessible from outside your network (Ağınızın dışından erişilebilecek olan bir uygulamayı yayımlama)** seçeneğini belirleyin. Bu seçeneği görmüyorsanız, Azure AD temel sahip veya Premium hello Kiracı içinde ayarlanan emin olun.
4. Merhaba seçeneklerin her biri aşağıdaki gibi tamamlayın:
 * **Ad**:--Örneğin, istediğiniz herhangi bir değer kullanmak **SharePoint**.
 * **İç URL**: hello hello SharePoint sitesinin URL'sini budur dahili olarak gibi **https://SharePoint/**. Bu örnekte, emin toouse olun **https**.
 * **Ön kimlik doğrulama yöntemi**: seçin **Azure Active Directory**.

  ![Bir uygulama eklemek için Seçenekler](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. Merhaba uygulama yayımlandıktan sonra hello tıklatın **yapılandırma** sekmesi.
6. Toohello seçeneği aşağı **üstbilgileri Çevir URL'de**. Merhaba varsayılan değer **Evet**. Çok değiştirme**Hayır**.

 SharePoint kullanan hello _ana bilgisayar üstbilgisi_ değeri toolook hello site. Aynı zamanda bu değere göre bağlantılar da oluşturur. Merhaba net etkisi toomake SharePoint oluşturur herhangi bir bağlantıyı toouse hello dış URL doğru olarak ayarlanmış bir yayımlanan URL olduğundan emin olur. Ayar Hello değeri çok**Evet** de etkinleştirir bağlayıcı tooforward hello isteği toohello arka uç uygulaması hello. Ancak, hello değeri çok ayarı**Hayır** bağlayıcı hello anlamına gelir hello iç ana bilgisayar adı değil gönderecek. Bunun yerine, URL toohello arka uç uygulaması Hello yayımlanmış olarak hello bağlayıcı hello ana bilgisayar üstbilgisi gönderir.

 Ayrıca, tooensure SharePoint kabul eder, bu URL, toocomplete hello SharePoint sunucusundaki bir daha fazla yapılandırma gerekir. Bu hello sonraki bölümde gerçekleştirirsiniz.

7. Değişiklik **iç kimlik doğrulama yöntemini** çok**tümleşik Windows kimlik doğrulaması**. Azure AD kiracınıza hello UPN şirket içinden farklı hello bulutta UPN kullanıyorsa, tooupdate unutmayın **oturum açma kimlik temsilcisi** de.
8. Ayarlama **iç uygulama SPN** daha önce belirlediğiniz toohello değeri. Örneğin, **http/sharepoint.demo.o365identity.us**.
9. Merhaba uygulama tooyour hedef kullanıcılar atayın.

Uygulamanızı benzer toohello örnek aşağıdaki gibi görünmelidir:

  ![Tamamlanan uygulama](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-hello-external-url"></a>Adım 3: SharePoint hello dış URL hakkında bilir emin olun.

SharePoint hello dış URL temel alınarak hello site bulabilirsiniz ve böylece bu dış URL temel alınarak bağlantılar oluşturmaz, son adım tooensure. Bunun için diğer erişim eşleşmeleri hello SharePoint sitesi için yapılandırarak.

1. Açık hello **SharePoint 2013 Yönetim Merkezi** site.
2. Altında **sistem ayarlarını**seçin **yapılandırma diğer erişim eşleşmeleri**.

 Merhaba açılır **diğer erişim eşleşmeleri** kutusu.

  ![Diğer erişim eşleşmeleri kutusu](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. Hello aşağı açılan listesinde **alternatif erişim eşleme koleksiyonu**seçin **değişiklik alternatif erişim eşleme koleksiyonu**.
4. Örneğin, siteniz--seçin **SharePoint - 80**.

  ![Bir site seçme](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. Bir iç URL veya genel bir URL olarak tooadd hello URL yayımlanan seçebilirsiniz. Bu örnek, genel bir URL hello extranet kullanır.
6. ' I tıklatın **ortak URL'leri Düzenle** hello içinde **Extranet** , yol ve enter hello hello yolu yayımlanan hello önceki adımda olduğu gibi uygulama. Örneğin **https://sharepoint-iddemo.msappproxy.net**.

  ![Merhaba yolu girme](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. **Kaydet** düğmesine tıklayın.

 Artık hello SharePoint sitesi harici olarak Azure AD uygulama proxy'si aracılığıyla erişebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

- [Nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamalar](active-directory-application-proxy-get-started.md)
- [Azure AD uygulama proxy'si bağlayıcılar anlama](application-proxy-understand-connectors.md)
- [SharePoint 2016 ve Office Online Server Azure AD uygulama proxy'si ile uygulama yayımlama](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
