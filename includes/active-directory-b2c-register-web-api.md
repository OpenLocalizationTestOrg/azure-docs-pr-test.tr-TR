[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

web API, tooregister hello tablosunda belirtilen hello ayarlarını kullanın.

![Yeni web api’si için örnek kayıt ayarları](./media/active-directory-b2c-register-web-api/b2c-new-web-api-settings.png)

| Ayar      | Örnek değer  | Açıklama                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Ad** | Contoso B2C API’si | Girin bir **adı** API tooconsumers açıklar Merhaba uygulaması için. | 
| **Web uygulamasını / web API'sini dahil etme** | Evet | Web API’si için **Evet**’i seçin. |
| **Örtük akışa izin verme** | Evet | Uygulamanız **OpenID Connect oturum açma bilgilerini** kullanıyorsa [Evet](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md)’i seçin. |
| **Yanıt URL'si** | `https://localhost:44316/` | Yanıt URL'leri, Azure AD B2C'nin, uygulamanız tarafından istenen belirteçleri getirdiği uç noktalardır. [Uygun bir](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **Yanıt URL’si** girin. Bu örnekte, API’niz yereldir ve bağlantı noktası 44316’yı dinlemektedir. |
| **Uygulama Kimliği URI'si** | api | Merhaba uygulama kimliği URI'si web API için kullanılan hello tanımlayıcısıdır. Merhaba tam tanımlayıcı Hello etki alanıyla birlikte URI sizin için oluşturulur. |

Tıklatın **oluşturma** tooregister uygulamanızı.

Yeni kaydettiğiniz uygulamanızı hello B2C Kiracı için hello uygulamalar listesinde görüntülenir. Web API hello listeden seçin. Merhaba API'nin özellik bölmesinde görüntülenir.

![Web API’si özellikleri](./media/active-directory-b2c-register-web-api/b2c-web-api-properties.png)

Merhaba genel benzersiz Not **uygulama istemci Kimliğini**. Uygulamanızın kodda hello Kimliğini kullanın.
