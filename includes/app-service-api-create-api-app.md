
<span data-ttu-id="fe2a2-101">[az webapp create](/cli/azure/appservice/web#create) komutuyla `myAppServicePlan` App Service planında bir [API uygulaması](../articles/app-service-api/app-service-api-apps-why-best-platform.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fe2a2-101">Create a [API app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/appservice/web#create) command.</span></span> 

<span data-ttu-id="fe2a2-102">Web uygulaması, API'niz için bir barındırma alanı sağlar ve dağıtılan uygulamanın görüntülenebileceği bir URL sunar.</span><span class="sxs-lookup"><span data-stu-id="fe2a2-102">The web app provides a hosting space for your API and provides a URL to view the deployed app.</span></span>

<span data-ttu-id="fe2a2-103">Aşağıdaki komutta *\<app_name>* kısmını benzersiz bir adla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fe2a2-103">In the following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="fe2a2-104">`<app_name>` benzersiz değilse "Belirtilen <app_name> adına sahip web sitesi zaten var" hata iletisiyle karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="fe2a2-104">If `<app_name>` is not unique, you get the error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="fe2a2-105">Web uygulamasının varsayılan URL'si `https://<app_name>.azurewebsites.net` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="fe2a2-105">The default URL of the web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="fe2a2-106">Web uygulaması oluşturulduğunda Azure CLI aşağıda yer alan örnekteki gibi bilgiler gösterir:</span><span class="sxs-lookup"><span data-stu-id="fe2a2-106">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span>

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