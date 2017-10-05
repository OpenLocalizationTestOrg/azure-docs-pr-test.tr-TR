<span data-ttu-id="11e4b-101">[az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) komutuyla yerel Git dağıtımını web uygulamasında gerçekleşecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="11e4b-101">Configure local Git deployment to the web app with the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="11e4b-102">App Service, web uygulamasına içerik dağıtmak için FTP, yerel Git, GitHub, Visual Studio Team Services ve Bitbucket gibi çeşitli yolları destekler.</span><span class="sxs-lookup"><span data-stu-id="11e4b-102">App Service supports several ways to deploy content to a web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="11e4b-103">Bu hızlı başlangıç için yerel Git’i kullanarak dağıtım gerçekleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11e4b-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="11e4b-104">Bu, yerel bir depodan Azure’daki bir depoya gönderim yapmak için bir Git komutunu kullanarak dağıtım yaptığınız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="11e4b-104">That means you deploy by using a Git command to push from a local repository to a repository in Azure.</span></span> 

<span data-ttu-id="11e4b-105">Aşağıdaki komutta *\<uygulama_adı>* kısmını web uygulamanızın adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="11e4b-105">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="11e4b-106">Çıktı aşağıdaki biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="11e4b-106">The output has the following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="11e4b-107">`<username>`, önceki adımlardan birinde oluşturduğunuz [dağıtım kullanıcısıdır](#configure-a-deployment-user).</span><span class="sxs-lookup"><span data-stu-id="11e4b-107">The `<username>` is the [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="11e4b-108">Bir sonraki adımda kullanmanız gerekeceğinden, gösterilen URI'yi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="11e4b-108">Copy the URI shown; you'll use it in the next step.</span></span>
