[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

Web API’nizi kaydetmek için tabloda belirtilen ayarları kullanın.

![Yeni web api’si için örnek kayıt ayarları](./media/active-directory-b2c-register-web-api/b2c-new-web-api-settings.png)

| Ayar      | Örnek değer  | Açıklama                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Ad** | Contoso B2C API’si | API’nizi tüketicilere açıklayacak bir **Ad** girin. | 
| **Web uygulamasını / web API'sini dahil etme** | Evet | Web API’si için **Evet**’i seçin. |
| **Örtük akışa izin verme** | Evet | Uygulamanız **OpenID Connect oturum açma bilgilerini** kullanıyorsa [Evet](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md)’i seçin. |
| **Yanıt URL'si** | `https://localhost:44316/` | Yanıt URL'leri, Azure AD B2C'nin, uygulamanız tarafından istenen belirteçleri getirdiği uç noktalardır. [Uygun bir](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **Yanıt URL’si** girin. Bu örnekte, API’niz yereldir ve bağlantı noktası 44316’yı dinlemektedir. |
| **Uygulama Kimliği URI'si** | api | Uygulama Kimliği URI’si, web API’niz için kullanılan tanımlayıcıdır. Tam etki alanı ile birlikte URI tanımlayıcısı sizin için oluşturulur. |

Uygulamanızı kaydetmek için **Create (Oluştur)** seçeneğine tıklayın.

Yeni kaydettiğiniz uygulamanız B2C kiracısı için uygulamalar listesinde görüntülenir. Listeden web API’nizi seçin. API’nin özellik bölmesi görüntülenir.

![Web API’si özellikleri](./media/active-directory-b2c-register-web-api/b2c-web-api-properties.png)

Genel benzersiz **Uygulama İstemci Kimliğini** not alın. Bu kimliği uygulamanızın kodlarında kullanırsınız.