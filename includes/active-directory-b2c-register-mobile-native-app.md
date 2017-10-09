[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister, mobil veya yerel uygulama hello tablosunda belirtilen hello ayarları kullanın.

![Yeni mobil veya yerel uygulama için örnek kayıt ayarları](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| Ayar      | Örnek değer  | Açıklama                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Ad** | Contoso B2C uygulaması | Girin bir **adı** uygulama tooconsumers açıklar Merhaba uygulaması için. |
| **Yerel istemci** | Evet | Mobil veya yerel bir uygulama için **Evet**’i seçin. |
| **Özel yeniden yönlendirme URI'si** | `com.onmicrosoft.contoso.appname://redirect/path` | Özel bir düzen ile yeniden yönlendirme URI’si girin. [İyi bir yeniden yönlendirme URI’si](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri) seçtiğinizden emin olun ve alt çizgi gibi özel karakterler kullanmayın. |

Tıklatın **oluşturma** tooregister uygulamanızı.

Yeni kaydettiğiniz uygulamanızı hello B2C Kiracı için hello uygulamalar listesinde görüntülenir. Mobil veya yerel uygulamanızı hello listeden seçin. Merhaba uygulamanın özellik bölmesinde görüntülenir.

![Uygulama özellikleri](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

Merhaba genel benzersiz Not **uygulama istemci Kimliğini**. Uygulamanızın kodda hello Kimliğini kullanın.

Yerel uygulamanız Azure AD B2C tarafından güvence altına alınmış bir web API'sini çağırıyorsa, aşağıdaki adımları gerçekleştirin:
   1. Giden toohello tarafından bir uygulama gizli anahtarı oluşturmak **anahtarları** dikey ve hello tıklayarak **anahtarı oluştur** düğmesi. Merhaba Not **uygulama anahtarı** değeri. Uygulamanızın kodda hello uygulama gizli anahtarı olarak hello değerini kullanın.
   2. **API Erişimi**’ne ve **Ekle**’ye tıklayıp web API’si ve kapsamlarınızı (izinler) seçin.

> [!NOTE]
> **Uygulama Gizli Anahtarı** önemli bir güvenlik kimlik bilgisidir ve güvenliği uygun şekilde sağlanmalıdır.
> 
