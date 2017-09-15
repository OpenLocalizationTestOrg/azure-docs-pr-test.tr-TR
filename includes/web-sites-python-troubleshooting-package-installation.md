<span data-ttu-id="1796a-101">Bazı paketler, Azure üzerinde çalıştığında pip kullanılarak yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="1796a-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="1796a-102">En basit haliyle, paket Python Paket Dizini’nde bulunmayabilir.</span><span class="sxs-lookup"><span data-stu-id="1796a-102">It may simply be that the package is not available on the Python Package Index.</span></span>  <span data-ttu-id="1796a-103">Derleyici gerekiyor olabilir (Azure App Service’te web uygulaması çalıştıran makinede derleyici olmayabilir).</span><span class="sxs-lookup"><span data-stu-id="1796a-103">It could be that a compiler is required (a compiler is not available on the machine running the web app in Azure App Service).</span></span>

<span data-ttu-id="1796a-104">Bu bölümde, bu sorunu düzeltmenin yollarını inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="1796a-104">In this section, we'll look at ways to deal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="1796a-105">Tekerlek isteği</span><span class="sxs-lookup"><span data-stu-id="1796a-105">Request wheels</span></span>
<span data-ttu-id="1796a-106">Paket yüklemesine bir derleyici gerekiyorsa, paket sahibinden pakete tekerleri de katmasını istemek için görüşmeye çalışmalısınız.</span><span class="sxs-lookup"><span data-stu-id="1796a-106">If the package installation requires a compiler, you should try contacting the package owner to request that wheels be made available for the package.</span></span>

<span data-ttu-id="1796a-107">Son kullanılabilirliği ile [Python 2.7 için Microsoft Visual C++ derleyicisi][Microsoft Visual C++ Compiler for Python 2.7], Python 2.7 için yerel koda sahip paketleri oluşturmak artık kolaydır.</span><span class="sxs-lookup"><span data-stu-id="1796a-107">With the recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier to build packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="1796a-108">Tekerlek derleme (Windows gerekir)</span><span class="sxs-lookup"><span data-stu-id="1796a-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="1796a-109">Not: Bu seçenek kullanıldığında, Azure App Service’in web uygulamasında kullanılan platform/mimari/sürümle eşleşen Python ortamı kullanılarak paketin derlendiğinden emin olun (Windows/32-bit/2.7 veya 3.4).</span><span class="sxs-lookup"><span data-stu-id="1796a-109">Note: When using this option, make sure to compile the package using a Python environment that matches the platform/architecture/version that is used on the web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="1796a-110">Tekerlek gerektiğinden paket yüklenmediyse, derleyiciyi yerel makinenize yükleyip paket için bir tekerlek derleyebilirsiniz; bundan sonra depoda yerini alacaktır.</span><span class="sxs-lookup"><span data-stu-id="1796a-110">If the package doesn't install because it requires a compiler, you can install the compiler on your local machine and build a wheel for the package, which you will then include in your repository.</span></span>

<span data-ttu-id="1796a-111">Mac/Linux kullanıcıları: Windows makinesine erişiminiz yoksa bkz [çalıştıran sanal makine Windows oluşturma] [ Create a Virtual Machine Running Windows] Azure üzerinde bir VM oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1796a-111">Mac/Linux Users: If you don't have access to a Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how to create a VM on Azure.</span></span>  <span data-ttu-id="1796a-112">Tekerlekleri derlemek için bunu kullanabilir, bunları depoya ekleyebilir ve isterseniz VM’yi atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1796a-112">You can use it to build the wheels, add them to the repository, and discard the VM if you like.</span></span> 

<span data-ttu-id="1796a-113">Python 2.7 için yüklediğiniz [Python 2.7 için Microsoft Visual C++ derleyicisi][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="1796a-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="1796a-114">Python 3.4 için yüklediğiniz [Microsoft Visual C++ 2010 Express'in][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="1796a-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="1796a-115">Tekerlekleri derlemek için tekerlek paketi gerekir:</span><span class="sxs-lookup"><span data-stu-id="1796a-115">To build wheels, you'll need the wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="1796a-116">Bağımlılığı derlemek için `pip wheel` öğesini kullanacaksınız:</span><span class="sxs-lookup"><span data-stu-id="1796a-116">You'll use `pip wheel` to compile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="1796a-117">Bu \wheelhouse klasöründe bir .whl dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1796a-117">This creates a .whl file in the \wheelhouse folder.</span></span>  <span data-ttu-id="1796a-118">\Wheelhouse klasörünü ve tekerlek dosyalarını deponuza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1796a-118">Add the \wheelhouse folder and wheel files to your repository.</span></span>

<span data-ttu-id="1796a-119">`--find-links` seçeneğini en üstüne eklemek amacıyla requirements.txt dosyanızı düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="1796a-119">Edit your requirements.txt to add the `--find-links` option at the top.</span></span> <span data-ttu-id="1796a-120">Bu, pip’ye python paket dizinine gitmeden önce yerel klasörde tam bir eşleşme aramasını bildirir.</span><span class="sxs-lookup"><span data-stu-id="1796a-120">This tells pip to look for an exact match in the local folder before going to the python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="1796a-121">Tüm bağımlılıklarınızı \Wheelhouse klasörüne eklemek ve python paket dizinini hiçbir şekilde kullanmamak isterseniz, requirements.txt dosyanızın en üstüne `--no-index` ekleyerek pip’yi paket dizinini yok sayması için zorlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1796a-121">If you want to include all your dependencies in the \wheelhouse folder and not use the python package index at all, you can force pip to ignore the package index by adding `--no-index` to the top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="1796a-122">Yüklemeyi özelleştirme</span><span class="sxs-lookup"><span data-stu-id="1796a-122">Customize installation</span></span>
<span data-ttu-id="1796a-123">easy\_install gibi alternatif bir yükleyici kullanarak sanal ortama paket yüklemek için dağıtım betiğini özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1796a-123">You can customize the deployment script to install a package in the virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="1796a-124">Açıklama satırı yapılan bir örnek için deploy.cmd dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="1796a-124">See deploy.cmd for an example that is commented out.</span></span>  <span data-ttu-id="1796a-125">pip’in bunları yüklenmesini önlemek için requirements.txt dosyasında bu gibi paketlerin listelenmediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1796a-125">Make sure that such packages aren't listed in requirements.txt, to prevent pip from installing them.</span></span>

<span data-ttu-id="1796a-126">Bunu dağıtım betiğine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1796a-126">Add this to the deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="1796a-127">Bir exe yükleyiciden yükleme yapacak easy\_install öğesini de kullanabilirsiniz (bunlardan bazıları zip uyumludur; bu nedenle easy\_install bunları destekler).</span><span class="sxs-lookup"><span data-stu-id="1796a-127">You may also be able to use easy\_install to install from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="1796a-128">Yükleyiciyi depoya ekleyin ve yolu yürütülebilir dosyaya geçirerek easy\_install öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1796a-128">Add the installer to your repository, and invoke easy\_install by passing the path to the executable.</span></span>

<span data-ttu-id="1796a-129">Bunu dağıtım betiğine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1796a-129">Add this to the deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-the-virtual-environment-in-the-repository-requires-windows"></a><span data-ttu-id="1796a-130">Sanal ortamı depoya ekleme (Windows gerekir)</span><span class="sxs-lookup"><span data-stu-id="1796a-130">Include the virtual environment in the repository (requires Windows)</span></span>
<span data-ttu-id="1796a-131">Not: Bu seçenek kullanıldığında, Azure App Service’in web uygulamasında kullanılan platform/mimari/sürümle eşleşen sanal ortam kullanıldığından emin olun (Windows/32-bit/2.7 veya 3.4).</span><span class="sxs-lookup"><span data-stu-id="1796a-131">Note: When using this option, make sure to use a virtual environment that matches the platform/architecture/version that is used on the web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="1796a-132">Sanal ortamı depoya eklerseniz, dağıtım betiğinin boş bir dosya oluşturarak Azure’da sanal ortamı yönetimi gerçekleştirmesine engel olabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1796a-132">If you include the virtual environment in the repository, you can prevent the deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="1796a-133">Sanal ortam otomatik olarak yönetildiği sırada kalan dosyaları engellemek için uygulamada var olan sanal ortamı silmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="1796a-133">We recommend that you delete the existing virtual environment on the app, to prevent leftover files from when the virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
