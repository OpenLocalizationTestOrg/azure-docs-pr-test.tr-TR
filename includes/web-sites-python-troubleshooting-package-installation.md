<span data-ttu-id="206e5-101">Bazı paketler, Azure üzerinde çalıştığında pip kullanılarak yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="206e5-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="206e5-102">Yalnızca bu hello paket Python paket dizinini hello üzerinde kullanılamıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="206e5-102">It may simply be that hello package is not available on hello Python Package Index.</span></span>  <span data-ttu-id="206e5-103">Derleyici gerekiyor olabilir (derleyici hello makine çalışan hello web uygulamasını Azure App Service mevcut değildir).</span><span class="sxs-lookup"><span data-stu-id="206e5-103">It could be that a compiler is required (a compiler is not available on hello machine running hello web app in Azure App Service).</span></span>

<span data-ttu-id="206e5-104">Bu bölümde, biz Bu sorun yolları toodeal göreceğiz.</span><span class="sxs-lookup"><span data-stu-id="206e5-104">In this section, we'll look at ways toodeal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="206e5-105">Tekerlek isteği</span><span class="sxs-lookup"><span data-stu-id="206e5-105">Request wheels</span></span>
<span data-ttu-id="206e5-106">Merhaba paket yükleme bir derleyici gerekiyorsa Tekerlek hello paketi için kullanılabilir hale hello paket sahibi toorequest görüşmeye çalışmalısınız.</span><span class="sxs-lookup"><span data-stu-id="206e5-106">If hello package installation requires a compiler, you should try contacting hello package owner toorequest that wheels be made available for hello package.</span></span>

<span data-ttu-id="206e5-107">Merhaba son kullanılabilirliği ile [Python 2.7 için Microsoft Visual C++ derleyicisi][Microsoft Visual C++ Compiler for Python 2.7], Python 2.7 için yerel koda sahip daha kolay toobuild paketleri sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="206e5-107">With hello recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier toobuild packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="206e5-108">Tekerlek derleme (Windows gerekir)</span><span class="sxs-lookup"><span data-stu-id="206e5-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="206e5-109">Not: Bu seçenek kullanıldığında hello platform/mimari/hello web uygulamasını Azure App Service'te kullanılan sürümle eşleşen Python ortamı kullanılarak emin toocompile hello paket olun (Windows/32-bit/2.7 veya 3.4).</span><span class="sxs-lookup"><span data-stu-id="206e5-109">Note: When using this option, make sure toocompile hello package using a Python environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="206e5-110">Derleyici gerektirdiğinden hello paket yüklenmediyse hello derleyici yerel makinenize yükleyin ve ardından, depoda yerini alacaktır hello paketi için bir tekerlek derleme.</span><span class="sxs-lookup"><span data-stu-id="206e5-110">If hello package doesn't install because it requires a compiler, you can install hello compiler on your local machine and build a wheel for hello package, which you will then include in your repository.</span></span>

<span data-ttu-id="206e5-111">Mac/Linux kullanıcıları: erişim tooa Windows makinesine sahip değilseniz, bkz: [çalıştıran sanal makine Windows oluşturma] [ Create a Virtual Machine Running Windows] nasıl toocreate Azure üzerinde bir VM.</span><span class="sxs-lookup"><span data-stu-id="206e5-111">Mac/Linux Users: If you don't have access tooa Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how toocreate a VM on Azure.</span></span>  <span data-ttu-id="206e5-112">Toobuild hello Tekerlek kullanın, toohello deposunu ekleyin ve hello VM isterseniz atın.</span><span class="sxs-lookup"><span data-stu-id="206e5-112">You can use it toobuild hello wheels, add them toohello repository, and discard hello VM if you like.</span></span> 

<span data-ttu-id="206e5-113">Python 2.7 için yüklediğiniz [Python 2.7 için Microsoft Visual C++ derleyicisi][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="206e5-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="206e5-114">Python 3.4 için yüklediğiniz [Microsoft Visual C++ 2010 Express'in][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="206e5-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="206e5-115">toobuild Tekerlek hello Tekerlek paketi gerekir:</span><span class="sxs-lookup"><span data-stu-id="206e5-115">toobuild wheels, you'll need hello wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="206e5-116">Kullanacağınız `pip wheel` toocompile bir bağımlılık:</span><span class="sxs-lookup"><span data-stu-id="206e5-116">You'll use `pip wheel` toocompile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="206e5-117">Bu, hello \wheelhouse klasöründe bir .whl dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="206e5-117">This creates a .whl file in hello \wheelhouse folder.</span></span>  <span data-ttu-id="206e5-118">Merhaba \wheelhouse klasörünü ve Tekerlek dosyalarını tooyour deposu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="206e5-118">Add hello \wheelhouse folder and wheel files tooyour repository.</span></span>

<span data-ttu-id="206e5-119">Requirements.txt tooadd hello Düzenle `--find-links` hello üst seçeneği.</span><span class="sxs-lookup"><span data-stu-id="206e5-119">Edit your requirements.txt tooadd hello `--find-links` option at hello top.</span></span> <span data-ttu-id="206e5-120">Bu, devam eden toohello python paket dizinini önce hello yerel klasörde tam bir eşleşme PIP toolook bildirir.</span><span class="sxs-lookup"><span data-stu-id="206e5-120">This tells pip toolook for an exact match in hello local folder before going toohello python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="206e5-121">Tüm bağımlılıklarınızı hello \wheelhouse klasörünü ve kullanılmıyor hello python paketinde dizin hiç tooinclude istiyorsanız ekleyerek PIP tooignore hello paket dizini zorlayabilirsiniz `--no-index` requirements.txt dosyanızın en üstüne toohello.</span><span class="sxs-lookup"><span data-stu-id="206e5-121">If you want tooinclude all your dependencies in hello \wheelhouse folder and not use hello python package index at all, you can force pip tooignore hello package index by adding `--no-index` toohello top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="206e5-122">Yüklemeyi özelleştirme</span><span class="sxs-lookup"><span data-stu-id="206e5-122">Customize installation</span></span>
<span data-ttu-id="206e5-123">Merhaba dağıtım komut dosyası tooinstall hello sanal ortamdaki, alternatif bir yükleyici gibi kolay kullanarak bir paket özelleştirebilirsiniz\_yükleyin.</span><span class="sxs-lookup"><span data-stu-id="206e5-123">You can customize hello deployment script tooinstall a package in hello virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="206e5-124">Açıklama satırı yapılan bir örnek için deploy.cmd dosyasına bakın.  Requirements.txt, bunları yüklenmesini tooprevent PIP ne gibi paketlerin listelenmediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="206e5-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, tooprevent pip from installing them.</span></span>

<span data-ttu-id="206e5-125">Bu toohello dağıtım betiği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="206e5-125">Add this toohello deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="206e5-126">Kolay mümkün toouse de olabilir\_tooinstall bir exe Yükleyiciden yükleme (zip uyumludur; bu nedenle easy bazılarıdır\_install bunları destekler).</span><span class="sxs-lookup"><span data-stu-id="206e5-126">You may also be able toouse easy\_install tooinstall from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="206e5-127">Merhaba yükleyici tooyour deposunu ekleyin ve kolay çağırma\_hello yolu toohello yürütülebilir geçirerek yükleyin.</span><span class="sxs-lookup"><span data-stu-id="206e5-127">Add hello installer tooyour repository, and invoke easy\_install by passing hello path toohello executable.</span></span>

<span data-ttu-id="206e5-128">Bu toohello dağıtım betiği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="206e5-128">Add this toohello deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a><span data-ttu-id="206e5-129">Merhaba sanal ortamı (Windows gerekir) hello depoya ekleme</span><span class="sxs-lookup"><span data-stu-id="206e5-129">Include hello virtual environment in hello repository (requires Windows)</span></span>
<span data-ttu-id="206e5-130">Not: Bu seçenek kullanıldığında emin toouse hello platform/mimari/hello web uygulamasını Azure App Service'te kullanılan sürümle eşleşen sanal bir ortama olun (Windows/32-bit/2.7 veya 3.4).</span><span class="sxs-lookup"><span data-stu-id="206e5-130">Note: When using this option, make sure toouse a virtual environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="206e5-131">Merhaba sanal ortam hello depoya eklerseniz, hello dağıtım komut dosyası boş bir dosya oluşturarak azure'da sanal ortamı yönetimi gerçekleştirmesine engel olabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="206e5-131">If you include hello virtual environment in hello repository, you can prevent hello deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="206e5-132">Merhaba sanal ortam otomatik olarak yönetildiğinde var olan sanal ortamı hello uygulama, tooprevent kalan dosyalarından hello silme öneririz.</span><span class="sxs-lookup"><span data-stu-id="206e5-132">We recommend that you delete hello existing virtual environment on hello app, tooprevent leftover files from when hello virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
