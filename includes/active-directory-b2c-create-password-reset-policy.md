uygulamanızda sıfırlama tooenable hassas parola toocreate bir parola sıfırlama İlkesi gerekir. Bu hello Kiracı genelinde parola sıfırlama belirtilen seçeneği Not [burada](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md). Bu ilke başarılı tamamlanma hello tüketicileri parola sıfırlama sırasında geçtikleri ve uygulama hello belirteçleri Merhaba içeriğine alacak hello deneyimleri açıklanmaktadır.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Merhaba ilkeleri ayarları bölümünde **parola sıfırlama ilkeleri** tıklatıp **+ Ekle**.

![Oturum açma veya kaydolma İlkeleri'ni seçin ve hello Ekle düğmesini tıklatın](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

Bir ilke girin **adı** uygulama tooreference için. Örneğin, `SSPR` girin.

**Kimlik sağlayıcıları**’nı seçin ve **E-posta adresi kullanarak parola sıfırla**’yı işaretleyin. **Tamam** düğmesine tıklayın.

![Bir kimlik sağlayıcısı e-posta adresini kullanarak parola sıfırlama seçin ve hello Tamam düğmesini tıklatın](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

**Uygulama talepleri**’ni seçin. Başarılı parola sıfırlama deneyiminizi sonra geri tooyour uygulama hello yetkilendirme belirteçleri döndürmesini istediğiniz talep gönderilen seçin. Örneğin, **Kullanıcının Nesne Kimliği**’ni seçin.

![Bazı uygulama taleplerini seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

Tıklatın **oluşturma** tooadd hello ilkesi. Hello ilkesi olarak listelenen **B2C_1_SSPR**. Merhaba **B2C_1_** öneki eklenmiş toohello adıdır.

Açık hello İlkesi seçerek **B2C_1_SSPR**. Merhaba tablosunda belirtilen hello ayarlarını doğrulayın ardından tıklatın **Şimdi Çalıştır**.

![İlkeyi seçin ve çalıştırın.](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| Ayar      | Değer  |
| ------------ | ------ |
| **Uygulamalar** | Contoso B2C uygulaması |
| **Yanıt URL'sini seçin** | `https://localhost:44316/` |

Yeni bir tarayıcı sekmesi açar ve müşteri deneyimi, uygulamanızda hello parola sıfırlama doğrulayabilirsiniz.

> [!NOTE]
> İlke oluşturma tooa dakika sürer ve tootake etkisi güncelleştirir.
>
