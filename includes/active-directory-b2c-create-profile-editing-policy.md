<span data-ttu-id="14ae7-101">Uygulamanızda profili düzenlemeyi etkinleştirmek için bir ilke düzenleme profili oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="14ae7-101">To enable profile editing on your application, you will need to create a profile editing policy.</span></span> <span data-ttu-id="14ae7-102">Bu ilke, tüketicilerin profil düzenleme sırasında karşılaşacağı deneyimleri ve işlem başarıyla tamamlandığında uygulamanın alacağı belirteçlerin içeriğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="14ae7-102">This policy describes the experiences that consumers will go through during profile editing and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="14ae7-103">Ayarların ilkeler bölümünde **Profil düzenleme ilkeleri**’ni seçip **+ Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="14ae7-103">In the policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Profil düzenleme ilkelerini seçin ve Ekle düğmesine tıklayın](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="14ae7-105">Uygulamanızın başvuracağı ilke **Adını** girin.</span><span class="sxs-lookup"><span data-stu-id="14ae7-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="14ae7-106">Örneğin, `SiPe` girin.</span><span class="sxs-lookup"><span data-stu-id="14ae7-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="14ae7-107">**Kimlik sağlayıcıları**’nı seçin ve **Yerel Hesapla Oturum Aç**’ı işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="14ae7-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="14ae7-108">İsteğe bağlı olarak, zaten yapılandırılmışsa sosyal kimlik sağlayıcıları öğesini de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14ae7-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="14ae7-109">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="14ae7-109">Click **OK**.</span></span>

![Kimlik sağlayıcısı olarak Yerel Hesapla Oturum Aç’ı seçin ve Tamam düğmesine tıklayın](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="14ae7-111">**Profil öznitelikleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="14ae7-111">Select **Profile attributes**.</span></span> <span data-ttu-id="14ae7-112">Tüketicinin profilinde görüntüleyebileceği ve düzenleyebileceği öznitelikleri seçin.</span><span class="sxs-lookup"><span data-stu-id="14ae7-112">Choose attributes the consumer can view and edit in their profile.</span></span> <span data-ttu-id="14ae7-113">Örneğin, **Ülke/Bölge**, **Görünen Ad** ve **Posta Kodu**’nu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="14ae7-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="14ae7-114">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="14ae7-114">Click **OK**.</span></span>

![Bazı öznitelikleri seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="14ae7-116">**Uygulama talepleri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="14ae7-116">Select **Application claims**.</span></span> <span data-ttu-id="14ae7-117">Başarılı bir profil düzenleme deneyiminden sonra uygulamanıza geri gönderilen yetkilendirme belirteçlerinde döndürülmesini istediğiniz talepleri seçin.</span><span class="sxs-lookup"><span data-stu-id="14ae7-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful profile editing experience.</span></span> <span data-ttu-id="14ae7-118">Örneğin, **Görünen Ad** ve **Posta Kodu**’nu seçin.</span><span class="sxs-lookup"><span data-stu-id="14ae7-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Bazı uygulama taleplerini seçin ve Tamam düğmesine tıklayın.](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="14ae7-120">İlkeyi eklemek için **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="14ae7-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="14ae7-121">İlke **B2C_1_SiPe** olarak listelenir.</span><span class="sxs-lookup"><span data-stu-id="14ae7-121">The policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="14ae7-122">Ada **B2C_1_** öneki eklenir.</span><span class="sxs-lookup"><span data-stu-id="14ae7-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="14ae7-123">**B2C_1_SiPe** adını seçerek ilkeyi açın.</span><span class="sxs-lookup"><span data-stu-id="14ae7-123">Open the policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="14ae7-124">Tabloda belirtilen ayarlarını doğrulayın, ardından **Şimdi Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="14ae7-124">Verify the settings specified in the table then click **Run now**.</span></span>

![İlkeyi seçin ve çalıştırın.](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="14ae7-126">Ayar</span><span class="sxs-lookup"><span data-stu-id="14ae7-126">Setting</span></span>      | <span data-ttu-id="14ae7-127">Değer</span><span class="sxs-lookup"><span data-stu-id="14ae7-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="14ae7-128">**Uygulamalar**</span><span class="sxs-lookup"><span data-stu-id="14ae7-128">**Applications**</span></span> | <span data-ttu-id="14ae7-129">Contoso B2C uygulaması</span><span class="sxs-lookup"><span data-stu-id="14ae7-129">Contoso B2C app</span></span> |
| <span data-ttu-id="14ae7-130">**Yanıt URL'sini seçin**</span><span class="sxs-lookup"><span data-stu-id="14ae7-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="14ae7-131">Yeni bir tarayıcı sekmesi açılır. Buradan, profil düzenleme için yapılandırılan tüketici deneyimini doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14ae7-131">A new browser tab opens, and you can verify the profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="14ae7-132">İlke oluşturma ve güncelleştirmelerinin etkili olması bir dakika kadar alabilir.</span><span class="sxs-lookup"><span data-stu-id="14ae7-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>