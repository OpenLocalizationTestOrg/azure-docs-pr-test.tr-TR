## <a name="obtain-an-azure-resource-manager-token"></a>Bir Azure Resource Manager belirteç edinme
Azure Active Directory kaynakları hello Azure Resource Manager kullanarak gerçekleştirdiğiniz tüm hello görevler kimliğini doğrulaması gerekir. diğer yaklaşımlar görmek için hello burada gösterilen örnek parola kimlik doğrulaması kullanır, [Azure Resource Manager kimlik doğrulama istekleri][lnk-authenticate-arm].

1. Aşağıdaki kodu toohello hello eklemek **ana** Program.cs tooretrieve hello uygulama kimliği ve parola kullanarak Azure AD'den bir belirteç yöntemi.
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. Oluşturma bir **ResourceManagementClient** kullanan kodu toohello hello sonuna aşağıdaki hello ekleyerek belirteci hello nesne **ana** yöntemi:
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. Oluşturma veya bir başvuru için kullanmakta olduğunuz hello kaynak grubu elde:
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx