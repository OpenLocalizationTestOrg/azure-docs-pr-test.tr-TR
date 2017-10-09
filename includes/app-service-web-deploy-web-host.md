### <a name="app-service-plan"></a><span data-ttu-id="bdd50-101">App Service planı</span><span class="sxs-lookup"><span data-stu-id="bdd50-101">App Service plan</span></span>
<span data-ttu-id="bdd50-102">Merhaba web uygulamasını barındırmak için hello hizmet planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bdd50-102">Creates hello service plan for hosting hello web app.</span></span> <span data-ttu-id="bdd50-103">Hello aracılığıyla hello planının hello ad **hostingPlanName** parametresi.</span><span class="sxs-lookup"><span data-stu-id="bdd50-103">You provide hello name of hello plan through hello **hostingPlanName** parameter.</span></span> <span data-ttu-id="bdd50-104">Merhaba hello planının aynı konuma hello kaynak grubu için kullanılan hello konumdur.</span><span class="sxs-lookup"><span data-stu-id="bdd50-104">hello location of hello plan is hello same location used for hello resource group.</span></span> <span data-ttu-id="bdd50-105">Merhaba fiyatlandırma katmanı ve çalışan boyutu hello belirtilen **sku** ve **workerSize** parametreleri</span><span class="sxs-lookup"><span data-stu-id="bdd50-105">hello pricing tier and worker size are specified in hello **sku** and **workerSize** parameters</span></span>

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

