### <a name="create-a-nodejs-application"></a><span data-ttu-id="f53ad-101">Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f53ad-101">Create a Node.js application</span></span>

<span data-ttu-id="f53ad-102">`sender.js` adlı yeni bir JavaScript dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f53ad-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="f53ad-103">Merhaba geçiş NPM paket ekleme</span><span class="sxs-lookup"><span data-stu-id="f53ad-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="f53ad-104">Proje klasörünüzdeki bir Düğüm komut isteminden `npm install hyco-ws` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f53ad-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="f53ad-105">Toosend iletileri biraz kod yazma</span><span class="sxs-lookup"><span data-stu-id="f53ad-105">Write some code toosend messages</span></span>

1. <span data-ttu-id="f53ad-106">Merhaba aşağıdakileri ekleyin `constants` hello toohello üstündeki `sender.js` dosya.</span><span class="sxs-lookup"><span data-stu-id="f53ad-106">Add hello following `constants` toohello top of hello `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="f53ad-107">Sabitler toohello aşağıdaki hello eklemek `sender.js` hello karma bağlantı ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="f53ad-107">Add hello following constants toohello `sender.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="f53ad-108">Köşeli ayraçlar Hello yer tutucuları hello karma bağlantıyı oluştururken aldığınız hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f53ad-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="f53ad-109">`const ns`-Geçiş ad alanı hello.</span><span class="sxs-lookup"><span data-stu-id="f53ad-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="f53ad-110">Emin toouse hello tam ad alanı adı olmalıdır; Örneğin, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="f53ad-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="f53ad-111">`const path`-hello karma bağlantı hello adı.</span><span class="sxs-lookup"><span data-stu-id="f53ad-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="f53ad-112">`const keyrule`-hello hello SAS anahtarının adı.</span><span class="sxs-lookup"><span data-stu-id="f53ad-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="f53ad-113">`const key`-hello SAS anahtarı değeri.</span><span class="sxs-lookup"><span data-stu-id="f53ad-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="f53ad-114">Aşağıdaki kodu toohello hello eklemek `sender.js` dosyası:</span><span class="sxs-lookup"><span data-stu-id="f53ad-114">Add hello following code toohello `sender.js` file:</span></span>
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    <span data-ttu-id="f53ad-115">Sender.js dosyanız aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="f53ad-115">Here is what your sender.js file should look like:</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

