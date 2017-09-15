<span data-ttu-id="a778b-101">Azure, uygulamanızın **bu koşulların her ikisi de doğruysa** Python kullandığını saptayacaktır:</span><span class="sxs-lookup"><span data-stu-id="a778b-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="a778b-102">requirements.txt dosyası kök klasöründe</span><span class="sxs-lookup"><span data-stu-id="a778b-102">requirements.txt file in the root folder</span></span>
* <span data-ttu-id="a778b-103">.py dosyaları VEYA python belirten runtime.txt dosyası kök klasöründe</span><span class="sxs-lookup"><span data-stu-id="a778b-103">any .py file in the root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="a778b-104">Durum böyle olduğunda, aşağıdaki ek Python işlemlerinin yanı sıra dosyaların standart eşitlemesini gerçekleştiren Python’a özel bir dağıtım betiğini de kullanacaktır:</span><span class="sxs-lookup"><span data-stu-id="a778b-104">When that's the case, it will use a Python specific deployment script, which performs the standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="a778b-105">Sanal ortamın otomatik yönetimi</span><span class="sxs-lookup"><span data-stu-id="a778b-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="a778b-106">PIP kullanarak requirements.txt dosyasında listelenen paketlerin yüklenmesi</span><span class="sxs-lookup"><span data-stu-id="a778b-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="a778b-107">Seçili Python sürümü temelinde uygun web.config oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a778b-107">Creation of the appropriate web.config based on the selected Python version.</span></span>
* <span data-ttu-id="a778b-108">Django uygulamaları için statik dosyaları toplama</span><span class="sxs-lookup"><span data-stu-id="a778b-108">Collect static files for Django applications</span></span>

<span data-ttu-id="a778b-109">Betiği özelleştirmek zorunda kalmadan, varsayılan dağıtım adımlarının bazı yönlerini denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a778b-109">You can control certain aspects of the default deployment steps without having to customize the script.</span></span>

<span data-ttu-id="a778b-110">Python’a özel dağıtım adımlarını atlamak istiyorsanız bu boş dosyayı oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a778b-110">If you want to skip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="a778b-111">Django uygulamanız için statik dosya toplamayı atlamak istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="a778b-111">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango 

<span data-ttu-id="a778b-112">Dağıtım üzerinde daha fazla denetim için aşağıdaki dosyaları oluşturarak varsayılan dağıtım betiğini geçersiz kılabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a778b-112">For more control over deployment, you can override the default deployment script by creating the following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="a778b-113">Kullanabileceğiniz [Azure komut satırı arabirimi] [ Azure command-line interface] dosyaları oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="a778b-113">You can use the [Azure command-line interface][Azure command-line interface] to create the files.</span></span>  <span data-ttu-id="a778b-114">Bu komutu proje klasörünüzden kullanın:</span><span class="sxs-lookup"><span data-stu-id="a778b-114">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="a778b-115">Bu dosyalar olmadığında, Azure geçici bir dağıtım betiği oluşturur ve bunu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="a778b-115">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="a778b-116">Yukarıdaki komutla oluşturduğunuzun aynısıdır.</span><span class="sxs-lookup"><span data-stu-id="a778b-116">It is identical to the one you create with the command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
