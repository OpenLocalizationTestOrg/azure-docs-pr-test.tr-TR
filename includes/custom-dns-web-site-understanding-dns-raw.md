Merhaba etki alanı adı sistemi (DNS) olan hello kullanılan toolocate kaynaklardaki Internet. Örneğin, tarayıcınızda bir web uygulaması adresi girin veya bir web sayfası bir bağlantıya tıklayın, bir IP adresine DNS tootranslate hello etki alanını kullanır. Başlangıç IP adresi tür sokak adresi gibi ancak çok İnsan kolay değil. Örneğin, bir DNS adı gibi çok daha kolay tooremember **contoso.com** olduğu tooremember 192.168.1.88 veya 2001:0:4137:1f67:24a2:3888:9cce:fea3 gibi bir IP adresi.

Merhaba DNS sistem temel *kayıtları*. Kayıtları ilişkilendirmek belirli bir *adı*, gibi **contoso.com**, bir IP adresi ya da başka bir DNS adına sahip. Bir ad DNS arar bir web tarayıcısı gibi bir uygulama, hello kaydı bulur ve onun işaret kullandığında tooas adresi hello. İsteğe bağlı olarak Hello noktaları toois bir IP adresi değeri, hello tarayıcı bu değeri kullanın. Ardından tooanother DNS adı işaret ediyorsa, hello uygulama yeniden toodo çözünürlüğü vardır. Sonuç olarak, tüm ad çözümlemesi bir IP adresi sona erer.

App Service'te bir web uygulaması oluşturduğunuzda, bir DNS adı toohello web uygulaması otomatik olarak atanır. Bu ad hello biçimini alır  **&lt;yourwebappname&gt;. azurewebsites.net**. Olmadığından de bir sanal IP adresi kullanılabilir DNS oluşturma kaydettiğinde oluşturabilir ya da kayıtları bu noktası toohello **. azurewebsites.net**, veya toohello IP adresini işaret edebilir.

> [!NOTE]
> Başlangıç IP adresi, web uygulamanızın silerseniz ve web uygulamanızı yeniden oluşturun veya hello uygulama hizmeti planı modu da değiştirmem değiştirir**serbest** çok ayarlandıktan sonra**temel**, **paylaşılan**, veya **standart**.
> 
> 

Ayrıca kayıtları, her biri kendi işlevleri ve sınırlamaları, birden çok tür vardır, ancak web uygulamaları için biz yalnızca yaklaşık iki önemli *A* ve *CNAME* kaydeder.

### <a name="address-record-a-record"></a>Adres kaydı (kaydını)
Bir A kaydı bir etki alanı gibi eşleştirir **contoso.com** veya **www.contoso.com**, *veya bir joker karakter etki alanı* gibi  **\*. contoso.com**, tooan IP adresi. App Service'in web uygulamasında Hello durumda ya da hello hizmeti veya web uygulamanız için satın alınan belirli bir IP adresi, sanal IP hello.

bir A kaydı bir CNAME kaydı üzerinden Hello ana avantajları şunlardır:

* Bir kök etki alanı gibi eşleyebilirsiniz **contoso.com** tooan IP adresi; bu bir kayıtları kullanarak birçok kaydedicilerin yalnızca izin ver
* Gibi bir joker karakter kullanan bir giriş olabilir  **\*. contoso.com**, hangi işlemek birden çok alt etki alanı için istekleri gibi **mail.contoso.com**,  **blogs.contoso.com**, veya **www.contso.com**.

> [!NOTE]
> Bir A kaydı eşlenen beri tooa statik IP adresi otomatik olarak, web uygulamanızın değişiklikleri toohello IP adresi çözümlenemiyor. Web uygulamanız için özel etki alanı adı ayarlarını yapılandırırken bir IP adresi A kayıtları ile kullanım için sağlanır; Bu değeri silin ve web uygulamanızı yeniden oluşturun veya hello uygulama hizmeti planı modu tooback çok değiştirirseniz ancak değişebilir**serbest**.
> 
> 

### <a name="alias-record-cname-record"></a>Diğer ad kaydı (CNAME kaydı)
Bir CNAME kaydı eşleyen bir *belirli* gibi DNS adı **mail.contoso.com** veya **www.contoso.com**, tooanother (kurallı) etki alanı adı. App Service Web Apps Hello durumda hello hello kurallı etki alanı adı olan  **&lt;yourwebappname >. azurewebsites.net** , web uygulamanızın etki alanı adı. Bir kez oluşturduktan sonra hello CNAME hello için diğer ad oluşturur  **&lt;yourwebappname >. azurewebsites.net** etki alanı adı. Merhaba CNAME girişi toohello IP adresini çözümlenir,  **&lt;yourwebappname >. azurewebsites.net** etki alanı adı otomatik olarak hello web uygulamasının başlangıç IP adresi değişirse, tootake herhangi bir eylem değil Bu nedenle gerekir.

> [!NOTE]
> Bazı etki alanı kayıt yalnızca toomap alt etki alanları bir CNAME kaydı gibi kullanırken izin **www.contoso.com**ve değil kök adları gibi **contoso.com**. CNAME kayıtları hakkında daha fazla bilgi için şirketiniz tarafından sağlanan hello belgelerine bakın <a href="http://en.wikipedia.org/wiki/CNAME_record">CNAME kaydı Wikipedia girişinde hello</a>, veya hello <a href="http://tools.ietf.org/html/rfc1035">IETF etki alanı adları - uygulama ve belirtim</a> Belge.
> 
> 

### <a name="web-app-dns-specifics"></a>Web uygulaması DNS özellikleri
Bir A kaydını Web Apps ile kullanılması, toofirst aşağıdaki TXT kayıtları hello birini oluşturun:

* **Merhaba kök etki alanı için** -bir DNS TXT kaydını  **@**  çok  **&lt;yourwebappname&gt;. azurewebsites.net**.
* **Belirli bir alt etki alanı için** -bir DNS adı  **&lt;alt etki alanı >** çok**&lt;yourwebappname&gt;. azurewebsites.net**. Örneğin, **bloglar** hello bir kayıt içinse **blogs.contoso.com**.
* **Merhaba joker alt-dodmains için** -bir DNS TXT kaydını *** çok  **&lt;yourwebappname&gt;. azurewebsites.net**.

Bu TXT kayıt toouse çalıştığınız hello etki alanı kendi kullanılan tooverify bulunuyor. Bu ayrıca toohello sanal IP adresi, web uygulamanızın işaret eden toocreating bir kayıttır.

Başlangıç IP adresi Bul ve **. azurewebsites.net** adları gerçekleştirerek web uygulamanız için adımları hello:

1. Merhaba, tarayıcınızı açmak [Azure Portal](https://portal.azure.com).
2. Merhaba, **Web Apps** dikey penceresinde, web uygulamanızı hello adına tıklayın ve ardından **özel etki alanları** hello sayfasının hello Alttan.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Merhaba, **özel etki alanları** göreceğiniz dikey penceresinde hello sanal IP adresi. Bu bilgiler, DNS kayıtlarını oluştururken kullanılacak olarak Kaydet
   
    ![](./media/custom-dns-web-site/virtual-ip-address.png)
   
   > [!NOTE]
   > Özel etki alanı adları ile kullanılamaz bir **serbest** web app ve hello uygulama hizmeti planı çok yükseltmelisiniz**paylaşılan**, **temel**, **standart**, veya **Premium** katmanı. Merhaba uygulama hizmeti hakkında daha fazla bilgi için plan nasıl toochange hello fiyatlandırma katmanı, web uygulamanızın dahil olmak üzere, fiyatlandırma katmanlarına bkz [nasıl tooscale web uygulamaları](../articles/app-service-web/web-sites-scale.md).
   > 
   > 

