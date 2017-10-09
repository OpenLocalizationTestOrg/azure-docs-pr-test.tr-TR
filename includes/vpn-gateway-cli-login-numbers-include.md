1. <span data-ttu-id="e259f-101">Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="e259f-101">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="e259f-102">Oturum açma hakkında daha fazla bilgi için bkz. [Azure CLI 2.0'ı kullanmaya başlama](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e259f-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

  ```azurecli
  az login
  ```
2. <span data-ttu-id="e259f-103">Birden fazla Azure aboneliğiniz varsa, hello hesap için hello abonelikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="e259f-103">If you have more than one Azure subscription, list hello subscriptions for hello account.</span></span>

  ```azurecli
  az account list --all
  ```
3. <span data-ttu-id="e259f-104">Merhaba abonelik toouse istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="e259f-104">Specify hello subscription that you want toouse.</span></span>

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```