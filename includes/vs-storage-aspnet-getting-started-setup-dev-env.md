## <a name="set-up-hello-development-environment"></a><span data-ttu-id="2c20e-101">Merhaba geliştirme ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="2c20e-101">Set up hello development environment</span></span>

<span data-ttu-id="2c20e-102">Bu bölümde, bir denetleyicisi ekleme bir bağlı Hizmetleri bağlantısı ekleme bir ASP.NET MVC uygulaması oluşturma dahil olmak üzere, geliştirme ortamını ayarlama açıklanmaktadır ve ad alanı yönergeleri belirten hello gerekli.</span><span class="sxs-lookup"><span data-stu-id="2c20e-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying hello required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="2c20e-103">Bir ASP.NET MVC uygulaması projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c20e-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="2c20e-104">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="2c20e-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="2c20e-105">Seçin **Dosya -> Yeni Proje ->** hello ana menüden</span><span class="sxs-lookup"><span data-stu-id="2c20e-105">Select **File->New->Project** from hello main menu</span></span>

1. <span data-ttu-id="2c20e-106">Merhaba üzerinde **yeni proje** iletişim kutusunda, aşağıdaki şekilde vurgulanmış hello hello seçenekleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="2c20e-106">On hello **New Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![ASP.NET projesi oluşturma](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="2c20e-108">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2c20e-108">Select **OK**.</span></span>

1. <span data-ttu-id="2c20e-109">Merhaba üzerinde **yeni ASP.NET projesi** iletişim kutusunda, aşağıdaki şekilde vurgulanmış hello hello seçenekleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="2c20e-109">On hello **New ASP.NET Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![MVC belirtin](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="2c20e-111">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2c20e-111">Select **OK**.</span></span>

### <a name="use-connected-services-tooconnect-tooan-azure-storage-account"></a><span data-ttu-id="2c20e-112">Bağlantılı Hizmetler tooconnect tooan Azure depolama hesabı kullan</span><span class="sxs-lookup"><span data-stu-id="2c20e-112">Use Connected Services tooconnect tooan Azure storage account</span></span>

1. <span data-ttu-id="2c20e-113">Merhaba, **Çözüm Gezgini**hello projesine sağ tıklayın ve hello bağlam menüsünden seçin **Ekle -> Hizmet bağlı**.</span><span class="sxs-lookup"><span data-stu-id="2c20e-113">In hello **Solution Explorer**, right-click hello project, and from hello context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="2c20e-114">Merhaba üzerinde **bağlı hizmet Ekle** iletişim kutusunda **Azure Storage**ve ardından **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="2c20e-114">On hello **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![Bağlı hizmet iletişim kutusu](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="2c20e-116">Merhaba üzerinde **Azure Storage** iletişim kutusunda hello hangi toowork istediğiniz ve seçmek istediğiniz Azure depolama hesabı **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2c20e-116">On hello **Azure Storage** dialog, select hello desired Azure storage account with which you want toowork, and select **Add**.</span></span>
