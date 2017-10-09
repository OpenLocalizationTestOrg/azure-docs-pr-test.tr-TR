Etki alanı adınızı Hello kayıtlarını dağıtıldıktan sonra aşağıdakileri yapmalısınız özel etki alanı adınızı olabilir, tarayıcı tooverify mümkün toouse olması web uygulamanızı Azure App Service'te kullanılan tooaccess olabilir.

> [!NOTE]
> Merhaba DNS sistem aracılığıyla, CNAME toopropagate biraz zaman alabilir. Bir hizmeti gibi kullanabilir <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> CNAME hello tooverify kullanılabilir.
> 
> 

Trafik Yöneticisi uç noktası olarak web uygulamanızı eklemediyseniz, ad çözümlemesi çalışabilmesi hello özel etki alanı adı yollar tooTraffic Yöneticisi bunu yapmanız gerekir. Trafik Yöneticisi sonra tooyour web uygulaması yönlendirir. Merhaba bilgileri kullanın [ekleme veya silme uç noktaların](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd web uygulamanızı bir uç nokta Traffic Manager profilinize olarak.

> [!NOTE]
> Web uygulamanızı bir uç nokta eklerken listelenmemişse için yapılandırıldığından emin olun **standart** uygulama hizmeti planı modu. Kullanmalısınız **standart** sipariş toowork Traffic Manager ile web uygulamanız için modu.
> 
> 

1. Merhaba, tarayıcınızı açmak [Azure Portal](https://portal.azure.com).
2. Merhaba, **Web Apps** sekmesini seçin, web uygulamanızın hello adını tıklatın, **ayarları**ve ardından **özel etki alanları**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Merhaba, **özel etki alanları** dikey penceresinde tıklatın **ana bilgisayar adını eklemek**.
4. Kullanım hello **ana bilgisayar adı** metin kutuları tooenter hello trafik yöneticisi etki alanı adı tooassociate bu web uygulaması ile.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. Tıklatın **doğrulama** toosave hello etki alanı adı yapılandırma.
6. Tıklatarak bağlı **doğrulama** Azure etki alanı doğrulama iş akışı kazandırın. Bu etki alanı sahipliğini yanı sıra ana bilgisayar adı kullanılabilirlik ve rapor başarı veya hata toofix hello nasıl üzerinde Düzenleyici kılavuzluk ayrıntılı hata kontrol eder.    
7. Doğrulama başarılı bağlı **ana bilgisayar adını eklemek** düğmesi etkin olacak ve mümkün toohello Ata ana bilgisayar adı olacaktır. Şimdi bir tarayıcıda tooyour özel etki alanı adı gidin. Özel etki alanı adınızı kullanarak, uygulama çalışan görmelisiniz. 
   
   Merhaba özel etki alanı adı yapılandırma tamamlandıktan sonra hello listelenmez **etki alanı adları** , web uygulamanızın bölüm.

Bu noktada, tarayıcınızda mümkün tooenter hello trafik yöneticisi etki alanı adı olması ve başarıyla, tooyour web uygulaması sürdüğünü, bkz.

