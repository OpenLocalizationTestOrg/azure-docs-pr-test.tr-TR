### <a name="create-a-nodejs-application"></a><span data-ttu-id="123da-101">Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="123da-101">Create a Node.js application</span></span>

<span data-ttu-id="123da-102">`listener.js` adlı yeni bir JavaScript dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="123da-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="123da-103">Merhaba geçiş NPM paket ekleme</span><span class="sxs-lookup"><span data-stu-id="123da-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="123da-104">Proje klasörünüzdeki bir Düğüm komut isteminden `npm install hyco-ws` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="123da-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="123da-105">Tooreceive iletileri biraz kod yazma</span><span class="sxs-lookup"><span data-stu-id="123da-105">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="123da-106">Merhaba sabit toohello üstündeki aşağıdaki hello eklemek `listener.js` dosya.</span><span class="sxs-lookup"><span data-stu-id="123da-106">Add hello following constant toohello top of hello `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="123da-107">Sabitler toohello aşağıdaki hello eklemek `listener.js` hello karma bağlantı ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="123da-107">Add hello following constants toohello `listener.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="123da-108">Köşeli ayraçlar Hello yer tutucuları hello karma bağlantıyı oluştururken aldığınız hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="123da-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="123da-109">`const ns`-Geçiş ad alanı hello.</span><span class="sxs-lookup"><span data-stu-id="123da-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="123da-110">Emin toouse hello tam ad alanı adı olmalıdır; Örneğin, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="123da-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="123da-111">`const path`-hello karma bağlantı hello adı.</span><span class="sxs-lookup"><span data-stu-id="123da-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="123da-112">`const keyrule`-hello hello SAS anahtarının adı.</span><span class="sxs-lookup"><span data-stu-id="123da-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="123da-113">`const key`-hello SAS anahtarı değeri.</span><span class="sxs-lookup"><span data-stu-id="123da-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="123da-114">Aşağıdaki kodu toohello hello eklemek `listener.js` dosyası:</span><span class="sxs-lookup"><span data-stu-id="123da-114">Add hello following code toohello `listener.js` file:</span></span>
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    <span data-ttu-id="123da-115">Listener.js dosyanız şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="123da-115">Here is what your listener.js file should look like:</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

