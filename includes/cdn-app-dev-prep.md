## <a name="prerequisites"></a>Ön koşullar
Biz CDN yönetim kod yazmadan önce toodo bazı hazırlık tooenable ihtiyacımız bizim kod toointeract hello Azure Resource Manager ile.  toodo bunu yapmanız gerekir:

* Bir kaynak grubu toocontain hello Bu öğreticide oluşturuyoruz CDN profili oluştur
* Uygulamamız için Azure Active Directory tooprovide kimlik doğrulamasını yapılandırma
* Toohello kaynak grubu, Azure AD kiracısı kullanıcılardan yalnızca yetkili böylece bizim CDN profili ile etkileşim kurabilen izinleri uygula

### <a name="creating-hello-resource-group"></a>Merhaba kaynak grubu oluşturma
1. Merhaba günlüğüne [Azure Portal](https://portal.azure.com).
2. Hello tıklatın **yeni** hello üst sol düğmesine ve ardından **Yönetim**, ve **kaynak grubu**.

    ![Yeni bir kaynak grubu oluşturma](./media/cdn-app-dev-prep/cdn-new-rg-1-include.png)
3. Kaynak grubunuzun çağrısı *CdnConsoleTutorial*.  Aboneliğinizi seçin ve yakın bir konum seçin.  İsterseniz, hello tıklatabilirsiniz **PIN toodashboard** onay kutusunu toopin hello kaynak grubu toohello Panosu hello Portalı'nda.  Bu, daha kolay toofind daha sonra hale getirir.  Seçimlerinizi yaptıktan sonra tıklatın **oluşturma**.

    ![Adlandırma hello kaynak grubu](./media/cdn-app-dev-prep/cdn-new-rg-2-include.png)
4. Tooyour Pano sabitlerseniz kaydetmedi hello kaynak grubu oluşturduktan sonra bunu tıklayarak bulabilirsiniz **Gözat**, ardından **kaynak grupları**.  Merhaba kaynak grubu tooopen'ı tıklatın.  Not, **abonelik kimliği**.  Biz bunu daha sonra ihtiyacınız olacak.

    ![Adlandırma hello kaynak grubu](./media/cdn-app-dev-prep/cdn-subscription-id-include.png)

### <a name="creating-hello-azure-ad-application-and-applying-permissions"></a>Merhaba Azure AD uygulaması oluşturma ve izinleri uygulama
Azure Active Directory ile tooapp kimlik doğrulaması iki yaklaşım vardır: tek tek kullanıcılara veya bir hizmet sorumlusu. Bir hizmet sorumlusu benzer tooa hizmeti Windows hesabıdır.  Belirli bir kullanıcının izinleri toointeract hello CDN profilleri ile verme yerine biz yerine hello toohello hizmet sorumlusu izinleri.  Hizmet asıl adı, genellikle otomatik, etkileşimli olmayan işlemleri için kullanılır.  Bu öğretici bir etkileşimli konsol uygulaması yazma olsa bile, biz hello hizmet asıl yaklaşım odak.

Bir hizmet sorumlusu oluşturma Azure Active Directory Uygulama oluşturma dahil olmak üzere birkaç adımdan oluşur.  toodo Bu, çok yapacağız[Bu öğreticiyi izleyin](../articles/resource-group-create-service-principal-portal.md).

> [!IMPORTANT]
> Merhaba tüm hello adımlarda emin toofollow olması [bağlantılı Öğreticisi](../articles/resource-group-create-service-principal-portal.md).  Bu *son derece önemli* , tam olarak açıklandığı gibi tamamlayın.  Toonote emin olun, **kimliği Kiracı**, **Kiracı etki alanı adı** (genellikle bir *. onmicrosoft.com* etki alanı özel bir etki alanı belirtmediğiniz sürece), **istemci kimliği** , ve **istemci kimlik doğrulama anahtarı**bunları daha sonra ihtiyacımız gibi.  Çok dikkatli tooguard olması, **istemci kimliği** ve **istemci kimlik doğrulama anahtarı**, bu kimlik bilgileri olarak herkes tarafından tooexecute işlemler hello hizmet sorumlusu kullanılır.
>
> Yapılandırma çok kiracılı uygulama adlı toohello adım aldığınızda, seçin **Hayır**.
>
> Toohello adım ulaştıklarında [atamak uygulama toorole](../articles/azure-resource-manager/resource-group-create-service-principal-portal.md#assign-application-to-role), daha önce oluşturduğumuz kullanım hello kaynak grubu *CdnConsoleTutorial*, ancak hello yerine **okuyucu** rolü atayın Merhaba **CDN profili katkıda bulunan** rol.  Merhaba uygulama hello atadıktan sonra **CDN profili katkıda bulunan** kaynak grubunuz, dönüş toothis öğretici rolü. 
>
>

Hizmet asıl ve atanan hello oluşturduktan sonra **CDN profili katkıda bulunan** rol, hello **kullanıcılar** dikey penceresinde kaynak grubunuz için benzer toothis görünmelidir.

![Kullanıcılar dikey penceresi](./media/cdn-app-dev-prep/cdn-service-principal-include.png)

### <a name="interactive-user-authentication"></a>Etkileşimli kullanıcı kimlik doğrulaması
Bir hizmet sorumlusu yerine etkileşimli tek tek kullanıcı kimlik doğrulaması yerine olurdu, hello bir hizmet sorumlusu için çok benzer toothat işlemidir.  Aslında, toofollow gerekir hello aynı yordamı, ancak bazı küçük değişiklikler yapın.

> [!IMPORTANT]
> Yalnızca bir hizmet sorumlusu yerine toouse tek tek kullanıcı kimlik doğrulaması seçme, sonraki adımları izleyin.
>
>

1. Uygulamanızın, yerine oluştururken **Web uygulaması**, seçin **yerel uygulama**.

    ![Yerel uygulama](./media/cdn-app-dev-prep/cdn-native-application-include.png)
2. Merhaba sonraki sayfada, istenir bir **yeniden yönlendirme URI'si**.  Hello URI doğrulanması çalışmaz, ancak ne girdiğiniz unutmayın.  Buna daha sonra ihtiyacınız olacak.
3. Hiçbir gerek toocreate yoktur bir **istemci kimlik doğrulama anahtarı**.
4. Bir hizmet asıl toohello atama yerine **CDN profili katkıda bulunan** rolü tooassign bireysel kullanıcıları veya grupları yapacağız.  Bu örnekte, ı atadığınız görebilirsiniz *CDN Demo kullanıcı* toohello **CDN profili katkıda bulunan** rol.  

    ![Tek tek kullanıcı erişimi](./media/cdn-app-dev-prep/cdn-aad-user-include.png)
