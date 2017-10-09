Başlangıç zamanı kimlik doğrulama hataları çoğunu tutarsız veya hatalı yapılandırma ayarları neden. Aşağıda, şeyler toocheck için belirli bazı öneriler verilmiştir.

* Merhaba kaçırılması kaydetmedi emin olun **kaydetmek** her yerden düğmesine tıklayın. Bu genellikle kolay toodo olur ve bir portal sayfasında hello doğru değerlerinde aramanız, ancak bunlar aslında hello Azure ortamı veya Azure AD uygulaması kaydedilmemiş hello sonucudur.
* Hello yapılandırılmış ayarları için **uygulama ayarları** hello Azure portal dikey emin olun, hello API uygulaması ve web uygulaması hello ayarları girildiğinde seçilmedi doğru.  Ayrıca hello ayarları olarak girildiğinden emin olun **uygulama ayarları** ve **bağlantı dizeleri**hello iki bölümlerin hello biçimini benzer gibi.
* Kimlik doğrulama tooa JavaScript ön uç için indirme hello bildirim yeniden tooverify, `oauth2AllowImplicitFlow` başarıyla çok değiştirildi`true`.
* HTTPS URL'leri yapılandırılmış her yerde kullanılan doğrulayın:
  
  * Proje kodda
  * CORS içinde
  * Her bir API uygulaması ve web uygulaması için Azure ortamı uygulaması ayarları içinde
  * Azure AD uygulama ayarları.
    
    Merhaba Portalı'ndan bir API uygulamasının URL'si kopyalarsanız, genellikle olduğunu unutmayın `http://` ve çok değiştirmek toomanually sahip`https://`.
* Kod değişiklikleri başarıyla dağıtıldı emin olun. Örneğin, bir birden çok proje çözümü bir proje kullanıcının kod ve toodeploy hello değişiklik düşünüyorsanız yanlışlıkla hello başkalarının birini olası toochange olur.
* Tarayıcınızda HTTP URL'lerini tooHTTPS URL'leri giderek emin olun. Varsayılan olarak, Visual Studio oluşturur HTTP URL'lerini profilleriyle yayımlama ve proje dağıttıktan sonra ne hello tarayıcısında açar.
* Kimlik doğrulama tooa JavaScript ön uç için CORS JavaScript kodu çağrılarını hello hello API uygulaması üzerinde doğru şekilde yapılandırıldığından emin olun. CORS ile ilgili hello sorun olup olmadığı hakkında emin değilseniz, deneyin "*" Merhaba kaynak URL'sini izin olarak. 
* JavaScript ön uç için tarayıcınızın geliştirici araçları konsolunu sekmesini tooget daha fazla hata bilgisi açın ve hello ağ HTTP isteklerini inceleyin. Ancak, konsol hata iletileri yanıltıcı olabilir. CORS hata belirten bir ileti alırsanız, kimlik doğrulaması hello gerçek sorunu olabilir. Geçici olarak geçici olarak devre dışı kimlik doğrulaması ile Merhaba uygulamayı çalıştırarak bu hello durumda olup olmadığını kontrol edebilirsiniz.
* .NET API uygulaması için elde kadar bilgi hata iletilerinde mümkün olduğunca ayarlayarak emin olun [customErrors modu tooOff](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remoteview).
* .NET API uygulaması için Başlat bir [uzaktan hata ayıklama oturumunun](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)ve bir taşıyıcı belirteci veya talep beklenen hello hizmet asıl kimliği karşı denetler kodu ADAL tooacquire kullanan toocode geçirilen hello değişkenlerin hello değerleri inceleyin Bu şekilde olası toofind beklenmeyen durumları olacak şekilde kodunuzu yapılandırma değerleri birçok farklı kaynaktan, çekme unutmayın. Örneğin, yanlış yazdınız, `ida:ClientId` olarak `ida:ClientID` Azure uygulama hizmeti ortamı ayarlarını yapılandırırken hello kod hello alabilirsiniz `ida:ClientId` hello Azure uygulama hizmeti ayarı yoksayılıyor hello Web.config dosyasından aradığı değeri. 
* Normal bir Internet Explorer penceresinde şeyler işe yaramazsa, bir varolan oturum açma engel olabilen; InPrivate ve Chrome ya da Firefox deneyin.

