<span data-ttu-id="d1cf0-101">Dağıtım kimlik bilgileri ile Merhaba oluşturun [az webapp dağıtım kullanıcısı ayarlanmadı](/cli/azure/webapp/deployment/user#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="d1cf0-101">Create deployment credentials with hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="d1cf0-102">Dağıtım kullanıcı FTP ve yerel Git dağıtım tooa web uygulaması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d1cf0-102">A deployment user is required for FTP and local Git deployment tooa web app.</span></span> <span data-ttu-id="d1cf0-103">Merhaba kullanıcı adı ve parola hesap düzeyindedir.</span><span class="sxs-lookup"><span data-stu-id="d1cf0-103">hello user name and password are account level.</span></span> <span data-ttu-id="d1cf0-104">_Bunlar Azure aboneliği kimlik bilgilerinizden farklıdır._</span><span class="sxs-lookup"><span data-stu-id="d1cf0-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="d1cf0-105">Komut, aşağıdaki Hello yerine  *\<kullanıcı adı >* ve  *\<parola >* yeni bir kullanıcı adı ve parola ile.</span><span class="sxs-lookup"><span data-stu-id="d1cf0-105">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="d1cf0-106">Merhaba kullanıcı adının benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1cf0-106">hello user name must be unique.</span></span> <span data-ttu-id="d1cf0-107">Merhaba parola en az sekiz karakter uzunluğunda, iki üç öğeleri aşağıdaki hello olmalıdır: harf, sayı, simge.</span><span class="sxs-lookup"><span data-stu-id="d1cf0-107">hello password must be at least eight characters long, with two of hello following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="d1cf0-108">Alırsanız bir ` 'Conflict'. Details: 409` hata, değişiklik hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="d1cf0-108">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="d1cf0-109">` 'Bad Request'. Details: 400` hatası alırsanız daha güçlü bir parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="d1cf0-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="d1cf0-110">Bu dağıtım kullanıcısını bir kez oluşturduktan sonra tüm Azure dağıtımlarınız için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1cf0-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="d1cf0-111">Kayıt hello kullanıcı adı ve parolası.</span><span class="sxs-lookup"><span data-stu-id="d1cf0-111">Record hello user name and password.</span></span> <span data-ttu-id="d1cf0-112">Bunları toodeploy hello web uygulaması daha sonra ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="d1cf0-112">You need them toodeploy hello web app later.</span></span>
>
>