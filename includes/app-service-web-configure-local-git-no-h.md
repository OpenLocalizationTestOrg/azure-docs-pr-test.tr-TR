<span data-ttu-id="059f4-101">Yerel Git dağıtım toohello web uygulaması ile Merhaba yapılandırma [az webapp dağıtım kaynağı config-yerel-git](/cli/azure/webapp/deployment/source#config-local-git) komutu.</span><span class="sxs-lookup"><span data-stu-id="059f4-101">Configure local Git deployment toohello web app with hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="059f4-102">Uygulama hizmeti çeşitli yolları toodeploy içerik tooa web uygulaması, FTP, yerel Git, GitHub, Visual Studio Team Services ve Bitbucket gibi destekler.</span><span class="sxs-lookup"><span data-stu-id="059f4-102">App Service supports several ways toodeploy content tooa web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="059f4-103">Bu hızlı başlangıç için yerel Git’i kullanarak dağıtım gerçekleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="059f4-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="059f4-104">Azure yerel deposu tooa depodan Git komut toopush kullanarak dağıtma anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="059f4-104">That means you deploy by using a Git command toopush from a local repository tooa repository in Azure.</span></span> 

<span data-ttu-id="059f4-105">Komut, aşağıdaki Hello yerine  *\<app_name >* web uygulamanızın ada sahip.</span><span class="sxs-lookup"><span data-stu-id="059f4-105">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="059f4-106">Merhaba çıktı biçimi aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="059f4-106">hello output has hello following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="059f4-107">Merhaba `<username>` hello olan [dağıtım kullanıcı](#configure-a-deployment-user) bir önceki adımda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="059f4-107">hello `<username>` is hello [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="059f4-108">Merhaba gösterilen URI kopyalayın; Merhaba sonraki adımda kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="059f4-108">Copy hello URI shown; you'll use it in hello next step.</span></span>
