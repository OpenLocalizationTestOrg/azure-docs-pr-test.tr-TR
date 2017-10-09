<span data-ttu-id="c4530-101">Oluşturma bir [web uygulaması](../articles/app-service-web/app-service-web-overview.md) hello içinde `myAppServicePlan` hello ile uygulama hizmeti planı [az webapp oluşturmak](/cli/azure/webapp#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="c4530-101">Create a [web app](../articles/app-service-web/app-service-web-overview.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="c4530-102">Merhaba web uygulaması bir barındırma alanı kodunuz için ve bir URL tooview dağıtılan hello uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4530-102">hello web app provides a hosting space for your code and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="c4530-103">Komut, aşağıdaki Hello yerine  *\<app_name >* benzersiz bir ad ile (geçerli karakterler `a-z`, `0-9`, ve `-`).</span><span class="sxs-lookup"><span data-stu-id="c4530-103">In hello following command, replace *\<app_name>* with a unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="c4530-104">Varsa `<app_name>` olan benzersiz değil, "< app_name > verilen ada sahip Web sitesi zaten var." Merhaba hata iletisini alırsınız</span><span class="sxs-lookup"><span data-stu-id="c4530-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="c4530-105">Merhaba hello web uygulamasının URL'sini varsayılan `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="c4530-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="c4530-106">Merhaba web uygulaması oluşturduğunuzda aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir:</span><span class="sxs-lookup"><span data-stu-id="c4530-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```

<span data-ttu-id="c4530-107">Toohello site toosee yeni oluşturulan web uygulamanız göz atın.</span><span class="sxs-lookup"><span data-stu-id="c4530-107">Browse toohello site toosee your newly created web app.</span></span>

```bash
http://<app_name>.azurewebsites.net
```
