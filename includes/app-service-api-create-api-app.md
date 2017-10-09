
Oluşturma bir [API uygulaması](../articles/app-service-api/app-service-api-apps-why-best-platform.md) hello içinde `myAppServicePlan` hello ile uygulama hizmeti planı [az webapp oluşturmak](/cli/azure/appservice/web#create) komutu. 

Merhaba web uygulaması barındırma alanı için API ve bir URL tooview dağıtılan hello uygulaması sağlar.

Komut, aşağıdaki Hello yerine  *\<app_name >* benzersiz bir ada sahip. Varsa `<app_name>` olan benzersiz değil, "< app_name > verilen ada sahip Web sitesi zaten var." Merhaba hata iletisini alırsınız Merhaba hello web uygulamasının URL'sini varsayılan `https://<app_name>.azurewebsites.net`. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Merhaba web uygulaması oluşturduğunuzda aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir:

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