Merhaba ile bir uygulama hizmeti planı oluştur [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) komutu.

[!INCLUDE [app-service-plan](app-service-plan.md)]

Merhaba aşağıdaki örnekte oluşturur adlı bir uygulama hizmeti planı `myAppServicePlan` hello içinde **serbest** fiyatlandırma katmanı:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Uygulama hizmeti planı Hello oluşturduğunuzda hello Azure CLI bilgi benzer toohello aşağıdaki örneğine gösterir:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "West Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
```