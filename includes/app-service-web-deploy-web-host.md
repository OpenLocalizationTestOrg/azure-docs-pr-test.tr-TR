### <a name="app-service-plan"></a>App Service planı
Merhaba web uygulamasını barındırmak için hello hizmet planı oluşturur. Hello aracılığıyla hello planının hello ad **hostingPlanName** parametresi. Merhaba hello planının aynı konuma hello kaynak grubu için kullanılan hello konumdur. Merhaba fiyatlandırma katmanı ve çalışan boyutu hello belirtilen **sku** ve **workerSize** parametreleri

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

