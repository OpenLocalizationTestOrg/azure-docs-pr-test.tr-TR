[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister web uygulamanızı hello tablosunda belirtilen hello ayarları kullanın.

![Yeni web uygulaması için örnek kayıt ayarları](./media/active-directory-b2c-register-web-app/b2c-new-app-settings.png)

| Ayar      | Örnek değer  | Açıklama                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Ad** | Contoso B2C uygulaması | Girin bir **adı** uygulama tooconsumers açıklar Merhaba uygulaması için. | 
| **Web uygulamasını / web API'sini dahil etme** | Evet | Web uygulaması için **Evet**’i seçin. |
| **Örtük akışa izin verme** | Evet | Uygulamanız **OpenID Connect oturum açma bilgilerini** kullanıyorsa [Evet](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md)’i seçin. |
| **Yanıt URL'si** | `https://localhost:44316` | Yanıt URL'leri, Azure AD B2C'nin, uygulamanız tarafından istenen belirteçleri getirdiği uç noktalardır. [Uygun bir](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **Yanıt URL’si** girin. Bu örnekte, uygulamanız yereldir ve bağlantı noktası 44316’yı dinlemektedir. |

Tıklatın **oluşturma** tooregister uygulamanızı.

Yeni kaydettiğiniz uygulamanızı hello B2C Kiracı için hello uygulamalar listesinde görüntülenir. Web uygulamanızı hello listeden seçin. Merhaba web uygulamasının özellik bölmesinde görüntülenir.

![Web uygulaması özellikleri](./media/active-directory-b2c-register-web-app/b2c-web-app-properties.png)

Merhaba genel benzersiz Not **uygulama istemci Kimliğini**. Uygulamanızın kodda hello Kimliğini kullanın.
