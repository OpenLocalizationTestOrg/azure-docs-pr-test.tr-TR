Merhaba etki alanı adı sistemi (DNS) olan hello kullanılan toolocate şeyler Internet. Örneğin, tarayıcınızda bir adres girin veya bir web sayfası bir bağlantıya tıklayın, bir IP adresine DNS tootranslate hello etki alanı kullanır. Başlangıç IP adresi tür sokak adresi gibi ancak çok İnsan kolay değil. Örneğin, bir DNS adı gibi çok daha kolay tooremember **contoso.com** olduğu tooremember 192.168.1.88 veya 2001:0:4137:1f67:24a2:3888:9cce:fea3 gibi bir IP adresi.

Merhaba DNS sistem temel *kayıtları*. Kayıtları ilişkilendirmek belirli bir *adı*, gibi **contoso.com**, bir IP adresi ya da başka bir DNS adına sahip. Bir ad DNS arar bir web tarayıcısı gibi bir uygulama, hello kaydı bulur ve onun işaret kullandığında tooas adresi hello. İsteğe bağlı olarak Hello noktaları toois bir IP adresi değeri, hello tarayıcı bu değeri kullanın. Ardından tooanother DNS adı işaret ediyorsa, hello uygulama yeniden toodo çözünürlüğü vardır. Sonuç olarak, tüm ad çözümlemesi bir IP adresi sona erer.

Bir Azure Web sitesi oluşturduğunuzda, bir DNS adı otomatik olarak toohello siteye atanır. Bu ad hello biçimini alır  **&lt;yoursitename&gt;. azurewebsites.net**. Web sitenizi bir Azure trafik Yöneticisi uç noktası olarak eklediğinizde, Web sitenizi sonra hello erişilebilen  **&lt;yourtrafficmanagerprofile&gt;. trafficmanager.net** etki alanı.

> [!NOTE]
> Web sitenizi bir trafik Yöneticisi uç noktası olarak yapılandırıldığında, hello kullanacağı **. trafficmanager.net** adresi DNS kayıtlarını oluştururken.
> 
> Trafik Yöneticisi ile CNAME kayıtlarına yalnızca kullanabilirsiniz
> 
> 

Ayrıca kayıtları, her biri kendi işlevleri ve sınırlamaları, birden çok tür vardır, ancak yapılandırılmış Web sitelerinde tooas trafik Yöneticisi uç noktaları için biz yalnızca yaklaşık bir dikkat edin; *CNAME* kaydeder.

### <a name="cname-or-alias-record"></a>CNAME veya diğer ad kaydı
Bir CNAME kaydı eşleyen bir *belirli* gibi DNS adı **mail.contoso.com** veya **www.contoso.com**, tooanother (kurallı) etki alanı adı. Azure trafik Yöneticisi'ni kullanarak Web Hello durumda hello hello kurallı etki alanı adı olan  **&lt;Uygulamam >. trafficmanager.net** Traffic Manager profilinizin etki alanı adı. Bir kez oluşturduktan sonra hello CNAME hello için diğer ad oluşturur  **&lt;Uygulamam >. trafficmanager.net** etki alanı adı. Merhaba CNAME girişi toohello IP adresini çözümlenir,  **&lt;Uygulamam >. trafficmanager.net** etki alanı adı otomatik olarak başlangıç IP adresi hello Web sitesinin değişirse tootake herhangi bir eylem elinizde şekilde.

Trafik Yöneticisi trafiği geldikten sonra hello trafiği tooyour Web sitesi hello Yük Dengeleme için yapılandırılan yöntemi kullanarak, ardından yönlendirir. Tamamen saydam toovisitors tooyour Web sitesidir. Tarayıcısında hello özel etki alanı adı yalnızca görürler.

> [!NOTE]
> Bazı etki alanı kayıt yalnızca toomap alt etki alanları bir CNAME kaydı gibi kullanırken izin **www.contoso.com**ve değil kök adları gibi **contoso.com**. CNAME kayıtları hakkında daha fazla bilgi için şirketiniz tarafından sağlanan hello belgelerine bakın <a href="http://en.wikipedia.org/wiki/CNAME_record">CNAME kaydı Wikipedia girişinde hello</a>, veya hello <a href="http://tools.ietf.org/html/rfc1035">IETF etki alanı adları - uygulama ve belirtim</a> Belge.
> 
> 

