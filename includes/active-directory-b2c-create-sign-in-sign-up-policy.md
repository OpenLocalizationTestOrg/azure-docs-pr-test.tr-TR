<span data-ttu-id="dc449-101">Uygulamanızda oturum açmayı etkinleştirmek için bir oturum açma ilkesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dc449-101">To enable sign-in on your application, you will need to create a sign-in policy.</span></span> <span data-ttu-id="dc449-102">Bu ilke, tüketicilerin profil düzenleme sırasında karşılaşacağı deneyimleri ve işlem başarıyla tamamlandığında uygulamanın alacağı belirteçlerin içeriğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="dc449-102">This policy describes the experiences that consumers will go through during sign-in and the contents of tokens that the application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="dc449-103">Ayarların ilkeler bölümünde **Oturum açma veya kaydolma ilkeleri**’ni seçip **+ Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dc449-103">In the policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![Oturum açma veya kaydolma ilkeleri’ni seçin ve Ekle düğmesine tıklayın.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="dc449-105">Uygulamanızın başvuracağı ilke **Adını** girin.</span><span class="sxs-lookup"><span data-stu-id="dc449-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="dc449-106">Örneğin, `SiUpIn` girin.</span><span class="sxs-lookup"><span data-stu-id="dc449-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="dc449-107">**Kimlik sağlayıcıları**’nı seçin ve **E-posta ile kaydolma**’yı işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="dc449-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="dc449-108">İsteğe bağlı olarak, zaten yapılandırılmışsa sosyal kimlik sağlayıcıları öğesini de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc449-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="dc449-109">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dc449-109">Click **OK**.</span></span>

![Kimlik sağlayıcısı olarak E-posta ile kaydolma’yı seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="dc449-111">**Kaydolma öznitelikleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="dc449-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="dc449-112">Tüketiciden kayıt sırasında toplamak istediğiniz öznitelikleri seçin.</span><span class="sxs-lookup"><span data-stu-id="dc449-112">Choose attributes you want to collect from the consumer during sign-up.</span></span> <span data-ttu-id="dc449-113">Örneğin, **Ülke/Bölge**, **Görünen Ad** ve **Posta Kodu**’nu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="dc449-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="dc449-114">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dc449-114">Click **OK**.</span></span>

![Bazı öznitelikleri seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="dc449-116">**Uygulama talepleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="dc449-116">Select **Application claims**.</span></span> <span data-ttu-id="dc449-117">Başarılı bir kayıt veya oturum açma deneyiminden sonra uygulamanıza geri gönderilen yetkilendirme belirteçlerinde döndürülmesini istediğiniz talepleri seçin.</span><span class="sxs-lookup"><span data-stu-id="dc449-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="dc449-118">Örneğin, **Görünen Ad**, **Kimlik Sağlayıcısı**, **Posta Kodu**, **Kullanıcı yeni** ve **Kullanıcının Nesne Kimliği**’ni işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="dc449-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![Bazı uygulama taleplerini seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="dc449-120">İlkeyi eklemek için **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dc449-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="dc449-121">İlke **B2C_1_SiUpIn** olarak listelenir.</span><span class="sxs-lookup"><span data-stu-id="dc449-121">The policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="dc449-122">Ada **B2C_1_** öneki eklenir.</span><span class="sxs-lookup"><span data-stu-id="dc449-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="dc449-123">**B2C_1_SiUpIn** adını seçerek ilkeyi açın.</span><span class="sxs-lookup"><span data-stu-id="dc449-123">Open the policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="dc449-124">Tabloda belirtilen ayarlarını doğrulayın, ardından **Şimdi Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dc449-124">Verify the settings specified in the table then click **Run now**.</span></span>

![İlkeyi seçin ve çalıştırın.](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="dc449-126">Ayar</span><span class="sxs-lookup"><span data-stu-id="dc449-126">Setting</span></span>      | <span data-ttu-id="dc449-127">Değer</span><span class="sxs-lookup"><span data-stu-id="dc449-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="dc449-128">**Uygulamalar**</span><span class="sxs-lookup"><span data-stu-id="dc449-128">**Applications**</span></span> | <span data-ttu-id="dc449-129">Contoso B2C uygulaması</span><span class="sxs-lookup"><span data-stu-id="dc449-129">Contoso B2C app</span></span> |
| <span data-ttu-id="dc449-130">**Yanıt URL'sini seçin**</span><span class="sxs-lookup"><span data-stu-id="dc449-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="dc449-131">Yeni bir tarayıcı sekmesi açılır. Buradan, oturum açma veya kaydolma için yapılandırılan tüketici deneyimini doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc449-131">A new browser tab opens, and you can verify the sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="dc449-132">İlke oluşturma ve güncelleştirmelerinin etkili olması bir dakika kadar alabilir.</span><span class="sxs-lookup"><span data-stu-id="dc449-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>