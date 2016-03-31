# 認證

## 簡介

Lumen 中的認證(Authentication)使用的是和 Laravel 相同的底層函式庫，但其架構上和完整的 Laravel framework 有的相當大的差異。
自從 Lumen 不支援 session state 之後，需要驗證的連入請求必須透過像是 API tokens 之類的無狀態機制進行驗證。

## 入門

#### 認證服務提供者

> **注意:** 在你使用 Lumen 提供的認證功能前，你應該要將 `bootstrap/app.php` 中的 `AuthServiceProvider` 取消註解。

`AuthServiceProvider` 位於 `app/Providers` 目錄，裡面應該包含了一個 `Auth::viaRequest` 的單一呼叫。 `viaRequest` 方法接受一個當需要認證的連入請求呼叫的閉包(Closure)。 在這個閉包(Closure)中, 你可以按照你的喜好去解析 `App\User` 實例。如果這個請求沒辦法找到任何一個已認證的使用者，該閉包(Closure)應該會回傳一個 `null`:

    $this->app['auth']->viaRequest('api', function ($request) {
    	// Return User or null...
    });

同樣，你一樣可以按照你的喜好去檢索已認證的使用者。 你可以在請求的標頭、查詢字串（請求中的一個bearer token）或是你的應用程式需要的任何其他方式使用API token。

#### 存取已認證使用者

和完整的 Laravel framework 一樣，你可以使用 `Auth::user()` 方法來檢索已認證的使用者。或者，你也可以在一個 `Illuminate\Http\Request` 實例中使用 `$request->user()` :

	use Illuminate\Http\Request;

	$app->get('/post/{id}', ['middleware' => 'auth', function (Request $request, $id) {
		$user = Auth::user();

		$user = $request->user();

		//
	}]);

> **注意:** 如果你希望使用 `Auth::user()` 來存取現在目前已認證的使用者，你應該要將 `bootstrap/app.php` 中的 `$app->withFacades()` 取消註解。

當然，任何你希望認證的路由都需要指定到 `auth` 這個 [middleware](/docs/{{version}}/middleware)，因此你需要將 `bootstrap/app.php` 中的  `$app->routeMiddleware()` 取消註解:

	$app->routeMiddleware([
	    'auth' => App\Http\Middleware\Authenticate::class,
	]);
