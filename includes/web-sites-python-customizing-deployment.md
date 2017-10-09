<span data-ttu-id="486c4-101">Azure, uygulamanızın **bu koşulların her ikisi de doğruysa** Python kullandığını saptayacaktır:</span><span class="sxs-lookup"><span data-stu-id="486c4-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="486c4-102">Requirements.txt dosyası hello kök klasöründe</span><span class="sxs-lookup"><span data-stu-id="486c4-102">requirements.txt file in hello root folder</span></span>
* <span data-ttu-id="486c4-103">hello kök klasöründe tüm .py dosyaları veya python belirten runtime.txt</span><span class="sxs-lookup"><span data-stu-id="486c4-103">any .py file in hello root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="486c4-104">Hello durum böyle olduğunda, hello gibi ek Python işlemlerinin yanı sıra dosyaların standart eşitlemesini gerçekleştiren bir Python belirli bir dağıtım betik kullanacaksınız:</span><span class="sxs-lookup"><span data-stu-id="486c4-104">When that's hello case, it will use a Python specific deployment script, which performs hello standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="486c4-105">Sanal ortamın otomatik yönetimi</span><span class="sxs-lookup"><span data-stu-id="486c4-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="486c4-106">PIP kullanarak requirements.txt dosyasında listelenen paketlerin yüklenmesi</span><span class="sxs-lookup"><span data-stu-id="486c4-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="486c4-107">Seçili Python versiyonunu hello üzerinde temel hello uygun web.config oluşturma.</span><span class="sxs-lookup"><span data-stu-id="486c4-107">Creation of hello appropriate web.config based on hello selected Python version.</span></span>
* <span data-ttu-id="486c4-108">Django uygulamaları için statik dosyaları toplama</span><span class="sxs-lookup"><span data-stu-id="486c4-108">Collect static files for Django applications</span></span>

<span data-ttu-id="486c4-109">Toocustomize hello betik gerek kalmadan hello varsayılan dağıtım adımları belirli yönlerini kontrol edebilir.</span><span class="sxs-lookup"><span data-stu-id="486c4-109">You can control certain aspects of hello default deployment steps without having toocustomize hello script.</span></span>

<span data-ttu-id="486c4-110">Tüm Python'a özel dağıtım adımlarını tooskip istiyorsanız bu boş dosyayı oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="486c4-110">If you want tooskip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="486c4-111">Dağıtım üzerinde daha fazla denetim için aşağıdaki dosyaları hello oluşturarak hello varsayılan dağıtım betiğini geçersiz kılabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="486c4-111">For more control over deployment, you can override hello default deployment script by creating hello following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="486c4-112">Merhaba kullanabilirsiniz [Azure komut satırı arabirimi] [ Azure command-line interface] toocreate hello dosyaları.</span><span class="sxs-lookup"><span data-stu-id="486c4-112">You can use hello [Azure command-line interface][Azure command-line interface] toocreate hello files.</span></span>  <span data-ttu-id="486c4-113">Bu komutu proje klasörünüzden kullanın:</span><span class="sxs-lookup"><span data-stu-id="486c4-113">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="486c4-114">Bu dosyalar olmadığında, Azure geçici bir dağıtım betiği oluşturur ve bunu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="486c4-114">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="486c4-115">Bir oluşturduğunuz yukarıdaki hello komutu ile aynı toohello olur.</span><span class="sxs-lookup"><span data-stu-id="486c4-115">It is identical toohello one you create with hello command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
