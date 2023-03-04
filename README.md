# MyReminderWeb

#
#### Laravel Where Not In
```php
$crashedCarIds = CrashedCar::pluck('car_id')->all();
$cars = Car::whereNotIn('id', $crashedCarIds)->select(...)->get();
```

#
#### Html Head Icon
```html
//public/img/logo-color-v2.png
<link rel="shortcut icon" href="{!! url('img/logo-color-v2.png') !!}" />
```

#
#### Html Select Dymanic Js

- [Source](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_select_add3)

- Example 1
```html
<div class="form-group">
  <label for="products_id">Product</label>
  <select name="products_id" id="products_id" class="form-control" aria-label="Default select example" required>
    <option disabled selected value="">Select Product</option>
  </select>
</div>
<br>
<div class="form-group">
  <label for="product_name">Product Name</label>
  <input type="text" class="form-control" id="product_name" name="product_name" placeholder="Product Name" required oninvalid="searchProduct('')" onkeyup="searchProduct('')" onchange="searchProduct('')" required>
</div>
<br>
<div class="row justify-content-end p-2">
  <button type="submit" class="btn btn-primary btn-sm">Submit</button>
</div>
```
- Example 2
```html
<div class="mb-3">
  <label class="form-label">Find Product</label>
  <div class="input-group mb-2">
    <input type="text" class="form-control" id="product_name" name="product_name" placeholder="Product Name" required oninvalid="searchProduct('')" onkeyup="searchProduct('')" onchange="searchProduct('')" required>

    <select name="products_id" id="products_id" class="form-control" aria-label="Default select example" required>
      <option disabled selected value="">Select Product</option>
    </select>
    <button class="btn" type="button" onclick="cariBarang()">Search</button>
  </div>
</div>
```
```php
public function findbynameall($name)
{
    $data = ProductsModel::where('product_name', 'like', "%$name%")->get();
    return json_encode($data);
}
```
```js
<script type="text/javascript">
  function searchProduct(data) {
    var product_name = document.getElementById("product_name").value;

    $.ajax({
      url: '/products/findbynameall/' + product_name,
      type: "GET",
      dataType: "JSON",
      success: function(data) {
      //array data data
        var x = document.getElementById("products_id");
        x.innerHTML = "";
        var optiondis = document.createElement("option");
        optiondis.text = "Select Product";
        optiondis.disabled = true;
        optiondis.selected = true;
        x.add(optiondis);

        for (let index = 0; index < data.length; index++) {
          const element = data[index];

          var option = document.createElement("option");
          option.text = element.product_name;
          option.value = element.id;
          x.add(option);
        }
      },
      error: function(jqXHR, textStatus, errorThrown) {
        alert('Gagal mendapatkan data');
      }
    });
  }
</script>
```

#
#### Ajax
```php
public function warningTask()
    {
        return [
            "data" => "asdsa"
        ];
    }
```
```php
Route::get('/home/warningtask', [HomeController::class, 'warningTask']);
```
```html
<script type="text/javascript">
    $(function() {
        warningTask();
    });

    function warningTask() {
        $.ajax({
            url: '/home/warningtask',
            type: "GET",
            dataType: "JSON",
            success: function(data) {
                alert(data.data)
            },
            error: function(jqXHR, textStatus, errorThrown) {
                alert('Gagal mendapatkan data' + errorThrown.message);
            }
        });
    }
</script>
```

#
#### PHP Date Space Count
```php
$earlier = new DateTime("2022-07-01");
$later = new DateTime("2022-07-04");

$data[$i]->waktu = $later->diff($earlier)->format("%a"); //3
```

#
#### LARAVEL IMG SRC PUBLIC
```php
<img class="cover header__photo-img" src="{{ url(''.$generatorList->img.'') }}">
```

#
#### PHP NATIV BASE URL IN INDEX
```php
<?php

function home_base_url()
{
  $base_url = (isset($_SERVER['HTTPS']) && $_SERVER['HTTPS'] != 'off') ? 'https://' : 'http://';
  $tmpURL = dirname(__FILE__);
  $tmpURL = str_replace(chr(92), '/', $tmpURL);
  $tmpURL = str_replace($_SERVER['DOCUMENT_ROOT'], '', $tmpURL);
  $tmpURL = ltrim($tmpURL, '/');
  $tmpURL = rtrim($tmpURL, '/');
  if (strpos($tmpURL, '/')) {
    $tmpURL = explode('/', $tmpURL);
    $tmpURL = $tmpURL[0];
  }
  if ($tmpURL !== $_SERVER['HTTP_HOST'])
    $base_url .= $_SERVER['HTTP_HOST'] . '/' . $tmpURL . '/';
  else
    $base_url .= $tmpURL . '/';
  return $base_url;
}

?>

<?php echo home_base_url(); ?>
```

#
#### Array Unik Duplicate Array PHP
```php
$out = Trans_product_outModel::select()->get();
$products_id = [];
for ($i = 0; $i < count($out); $i++) {
    $products_id[] = $out[$i]->products_id;
}
$products_id = array_unique($products_id);
$products_id = array_values($products_id);
```

#
#### Laravel Params Get
```php
{{ Request::segment(1) }}
{{ Request::path() }}
{{ request()->a }}
{{ app('request')->input('page') }}
{{ request()->get('date') }}
```
```js
const currentLocation = window.location + "";
const id = currentLocation.split('/');
id[5];

const queryString = window.location.search;
const urlParams = new URLSearchParams(queryString);
var date = urlParams.get('date'); ?date=2022-06-22
```

#
#### Laravel HtAccess

- .htaccess
```
<IfModule mod_rewrite.c>

RewriteEngine On

RewriteRule ^(.*)$ public/$1 [L]

</IfModule>
```

#
#### Laravel DataTables Custom Column

[Source](https://adinata-id.medium.com/server-side-datatables-menggunakan-yajra-1-pada-laravel-adminlte-c101f1276085)

```html
<link rel="stylesheet" href="https://cdn.datatables.net/1.11.5/css/dataTables.bootstrap4.min.css" />
<link rel="stylesheet" href="https://cdn.datatables.net/rowreorder/1.2.8/css/rowReorder.bootstrap4.min.css" />

<script src="https://code.jquery.com/jquery-3.5.1.js"></script>
<script src="https://cdn.datatables.net/1.11.5/js/jquery.dataTables.min.js"></script>
<script src="https://cdn.datatables.net/1.11.5/js/dataTables.bootstrap4.min.js"></script>
<script src="https://netdna.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>
<script src="https://cdn.datatables.net/rowreorder/1.2.8/js/dataTables.rowReorder.min.js"></script>
```

```html
<div class="col-12">
    <div class="card">
        <div class="card-header">
            <h3 class="card-title">List Data Products</h3>
        </div>
        <div class="card-body">
            <table class="table table-striped table-bordered" id="myDatatable" style="width: 100%;">
                <thead class="thead-dark">
                    <tr>
                        <th>No</th>
                        <td>Name</td>
                        <td>Active</td>
                        <td>Created at</td>
                        <td>Updated at</td>
                        <td>Action</td>
                    </tr>
                </thead>
                <tbody>
                </tbody>
            </table>
        </div>
    </div>
</div>
<script type="text/javascript">
    function paramsToJson(url) {
        var params = url.substring(url.indexOf("?"));
        var jsonData = "{";

        if (url.includes("?")) {
            params = params.replace("?", "");
            params = params.split("&");
            for (var i = 0; i < params.length; i++) {
                var d = params[i];
                d = d.split("=");
                jsonData += "\"" + d[0] + "\":\"" + d[1] + "\",";
            }
            jsonData = jsonData.slice(0, -1);
        } else {
            params = "";
        }
        jsonData += "}";
        return jsonData;
    }

    $(function() {
        var url = window.location.href;
        var jsonData = paramsToJson(url);
        var table = $('#myDatatable').DataTable({
            processing: true,
            serverSide: true,
            autowidth: false,
            scrollX: true,
            order: [
                [1, 'asc']
            ],
            ajax: {
                type: 'GET',
                url: "{{ route('products.data') }}",
                data: JSON.parse(jsonData)
            },
            columns: [{
                    data: 'DT_RowIndex',
                    name: 'DT_RowIndex',
                    orderable: false,
                    searchable: false,
                    width: '15px'
                },
                {
                    data: 'name',
                    name: 'name',
                },
                {
                    data: 'flag_active',
                    name: 'flag_active',
                    width: '30px',
                    render: function(data, type, row) {
                        if (data == 1) {
                            return '<span class="badge badge-sm bg-green text-uppercase ">Active</span>';
                        } else {
                            return '<span class="badge badge-sm bg-red text-uppercase ">Inactive</span>';
                        }
                    }
                },
                {
                    data: 'created_at',
                    name: 'created_at',
                    width: '125px'
                },
                {
                    data: 'updated_at',
                    name: 'updated_at',
                    width: '125px'
                },
                {
                    data: 'action',
                    name: 'action',
                    orderable: false,
                    searchable: false,
                    width: '125px'
                },
            ],
            language: {
                paginate: {
                    next: '&#8594;', // or '→'
                    previous: '&#8592;', // or '←'
                }
            }
        });
    });
</script>
```
```php
class ProductsController extends Controller
{
    //dataTables
    public function dataTables(Request $request)
    {
        if ($request->ajax()) {
            $data = $this->getData($request);

            return DataTables::of($data)
                ->addIndexColumn()
                ->addColumn('action', function ($row) {
                    $actionBtn = "<td>aksi</td>";
                    return $actionBtn;
                })
                ->rawColumns(['action'])
                ->make(true);
        }
    }

    public function getData(Request $request, $flag_active = "")
    {
        $date_start = $request->get("date_start");
        $date_end = $request->get("date_end");

        $data = ProductsModel::select();

        if ($flag_active != "") {
            $data = $data->where("products.flag_active", "=", $flag_active);
        }

        if ($date_start != "" && $date_end != "") {
            $data = $data->wherebetween("products.created_at", array($date_start . " 00:00:00", $date_end . " 23:59:59"));
        } else if ($date_start != "") {
            $data = $data->where("products.created_at", ">=", $date_start . " 00:00:00");
        } else if ($date_end != "") {
            $data = $data->where("products.created_at", "<=", $date_end . " 23:59:59");
        }

        $data = $data->orderBy('products.flag_active', 'desc');
        $data = $data->get();;

        return $data;
    }
}
```

#
#### Web Upload Foto
```php
//use Illuminate\Support\Str;
$file = $r->file('signature');
$tujuan_upload = 'storage/photo/staffs';
$generateName = Str::random(40) . "." . $file->getClientOriginalExtension();
$file->move($tujuan_upload, $generateName);
$photo = $tujuan_upload . "/" . $generateName;

$staff->signature = $photo;
```

#
#### forEach number no
```php
<?php $i = 0 ?>
@foreach ($aaa as $value)
<?php $i++ ?>
    <tr>
        <td>{{ $i}}</td>
        <td>{{$value->name}}</td>
    </tr>
@endforeach
```

#
#### TD Center
```html
<td style='text-align:center; vertical-align:middle'></td>
```

#
#### Ajax Alert Data Success
```js
$(function() {
    $.ajax({
        url: '/home/flmchart',
        type: "GET",
        dataType: "JSON",
        success: function(data) {
            alert(JSON.stringify(data));
        },
        error: function(jqXHR, textStatus, errorThrown) {
            alert('Gagal mendapatkan data');
        }
    });
});
```

#
#### Js Current Time Date
```js
var m = new Date();
var dateString =
    m.getUTCFullYear() + "/" +
    ("0" + (m.getUTCMonth()+1)).slice(-2) + "/" +
    ("0" + m.getUTCDate()).slice(-2) + " " +
    ("0" + m.getUTCHours()).slice(-2) + ":" +
    ("0" + m.getUTCMinutes()).slice(-2) + ":" +
    ("0" + m.getUTCSeconds()).slice(-2);

console.log(dateString);
```

#
#### Randomize (shuffle) JavaScript array JS
```js
const colors = ["#206bc4", "#4299e1", "#4263eb", "#ae3ec9", "#d6336c", "#d63939", "#f76707", "#f59f00", "#74b816", "#2fb344", "#0ca678", "#17a2b8", "#1e293b", "#626976"]
shuffle(colors);

//fun
function shuffle(array) {
    let currentIndex = array.length,
        randomIndex;

    // While there remain elements to shuffle.
    while (currentIndex != 0) {

        // Pick a remaining element.
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;

        // And swap it with the current element.
        [array[currentIndex], array[randomIndex]] = [
            array[randomIndex], array[currentIndex]
        ];
    }

    return array;
}
```

#
#### Laravel Route
```php
Route::group(['namespace' => 'App\Http\Controllers'], function () {
    Route::get('/', 'HomeController@index')->name('home.index');
});
```
```php
//laravel 8
use App\Http\Controllers\UserController;
Route::get('/users', [UserController::class, 'index']);
// or
Route::get('/users', 'App\Http\Controllers\UserController@index');
```
```php
use App\Http\Controllers\API\PagingControllerZein;
Route::prefix('paging')->group(function () {
     Route::get('/paging', [PagingControllerZein::class, 'paging']); //127.0.0.1:8000/api/paging/paging
});
```

#
#### Laravel Flash Message
```php
Route::prefix('barang')->group(function () {
    Route::get('/', [BarangController::class, 'index']); // /barang
});
```
```php
public function create(Request $r){
    BarangModel::create($r->all());
    return redirect('/barang')->with('sukses','Data berhasil diinput');
}
```
```php
@if(session('sukses'))
<div class="alert alert-success" role="alert">
  {{session('sukses')}}
</div>
@endif
```
```php
Request $r = $r->all();

if ($r->date != "")
    return Redirect::to('/data/report/' . $r->tools_id . '?date=' . $r->date)->with('sukses', 'Success Insert Data');
else
    return Redirect::to('/data/report/' . $r->tools_id)->with('sukses', 'Success Insert Data');
```
```
@if (\Session::has('success'))
    <div class="alert alert-success">
        <ul>
            <li>{!! \Session::get('success') !!}</li>
        </ul>
    </div>
@endif
```
```
var Sessiondescription = "{{ \Session::has('success') }}";
// var Sessiondescription = '@Session["success"]';
if (Sessiondescription.length > 0) {
    alert(Sessiondescription);
    showModalSuccess('Perhatian', '{{ Session::get('success') }}');
}
```

#
#### Laravel Route Name
```php
Route::prefix('barang')->group(function () {
    Route::get('/', [BarangController::class, 'index'])->name('barang.index');
    Route::post('/update', [BarangController::class, 'update'])->name('barang.update');
});
```
```php
<form action="{{ route('barang.update') }}" method="POST"></form>

<form action="/barang/update" method="POST"></form>
```
```html
<a href="/examples/export/{{Request::segment(3)}}?date={{request()->date}}" class="btn btn-yellow d-none d-sm-inline-block">
Export
</a>
```

#
#### If demo
```
String detail = "";
String type = "";
String reason = "";
String photo = "";
/*
true if all empty
false if one fill
*/

if (detail.length()==0 && type.length()==0 && reason.length()==0 && photo.length()==0){
    Log.d(TAG, "onCreate: true delete data");
} else {
    Log.d(TAG, "onCreate: false simpan/update data ");
}
```

#
#### Laravel Title
```html
@yield('sidebar', \View::make('defaultSidebar'))
```

#
#### Validate FileSize
```java
//return false if file size more than 20 mB
public boolean validateFileSize(String path) {
    File file = new File(path);

    long fileSizeInBytes = file.length();
    long fileSizeInKB = fileSizeInBytes / 1024;
    long fileSizeInMB = fileSizeInKB / 1024;

    return fileSizeInMB <= 20;
}
```

#
#### Laravel Auth Get Data
```php
{{ Auth::user()->id }}
```

#
#### Collection
```
Collections.sort(listFilter, new Comparator<DataItem>() {
    @Override
    public int compare(DataItem o1, DataItem o2) {
        return o1.getStrTv2().toLowerCase().compareTo(o2.getStrTv2().toLowerCase());
    }
});
```

#
#### PHP JSON To Object
```php
$rawJson = "{ post: { text: 'my text' } }";
$decodedAsArray = json_decode($rawJson, true);
$innerPost = $decodedAsArray['post'];

$post = new Post();
$post->forceFill($innerPost);
$post->save();
```

```php
$post = new Post();
foreach ($r->all() as $key => $value) {
    $post->$key = $value;
}
$post->save();
```

#
#### laravel Image Public
```html
<!-- public/uploads/myimage.jpg -->
<img src="{{url('/uploads/myimage.jpg')}}" alt="Image"/>
```

#
#### Laravel Public X Api X android
```
https://stackoverflow.com/questions/30675025/access-to-laravel-5-app-locally-from-an-external-device/30675683#30675683

php artisan serve --host 0.0.0.0
http://192.168.1.101:8000
php artisan serve --host 0.0.0.0 --port 80
http://192.168.1.101
```
https://demo-laravel.gzeinnumer.com/api/product/all
http://192.168.1.10:8000/api/product/all


#
#### Node JS Express JS Starter
```
mkdir project_my
npm init -y
npm install -S express ejs
npm app.js
```
```
const express = require('express')
const app = express()

app.get('/params_input', (req, res) => {
    //
})
```

#
#### Node JS Form Run Params
```
// var run = require('child_process');
// run.fork(path + '/tools/model.js', ["BarangController"]); const data = process.argv[2];

// require('shelljs').exec('node tools/templates/laravel_web/run.js', { body: req.body });
// require('shelljs').exec('node tools/templates/laravel_web/run.js');
```

#
#### Express JS Form
```js
app.post('/params_input', urlencodedParser, [

], (req, res) => {
    console.log('Got body:', req.body);
})
```
```html
<form action="/params_input" method="POST" novalidate>
    <div class="form-group">
        <label for="controllerName" class="form-label">controllerName</label>
        <input type="text" class="form-control" name="controllerName" id="controllerName">
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

#
#### Laravel Blade PHP Variable
```php
public function index(){
    $data = BarangModel::all();
    $sent = [
        'data' => $data,
        'find' => null
    ];
    return view('barang.index', $sent);
}
```
```html
<input name="id" @if(!empty($find)) value="{{$find->id}}" @endif>
```

#
#### SQL ORDER BY NO ID
```java
String query = "SELECT *, ROW_NUMBER() OVER() as LineNo  FROM " + table + " order by LineNo DESC;";
```

#
#### Laravel Key
```
php artisan key:generate
```

#
#### Laravel Public
```
http://localhost/laravel_project/public
```
or
```
http://localhost/mylogin/public
```
```
php artisan serve --host 0.0.0.0
```
```
http://192.168.1.3:8000/api/login
```

#
#### BottomNavigationView label always show
```xml
<com.google.android.material.bottomnavigation.BottomNavigationView
    ...
    app:labelVisibilityMode="labeled"
    app:menu="@menu/bottom_navigation_menu_v1" />
```

#
#### CI4 Redirect
```php
return redirect()->to('url');
return redirect()->route('named_route');
```

#
#### CI3 CI4 CodeIgnither Laravel

- CI3
```php
$sql = "select * from users order by id desc;";
$query = $this->db->query($sql);
return $query->result_array();
//echo $d['id'];;
```
- CI4
```php
$query = "SELECT * FROM product;";
$db = \Config\Database::connect();
$data = $db->query($query);

// return json_encode($data->getResult());
// return json_encode($query->getResultArray());
// return json_encode($query->getRow());
return $this->respond($data->getResult());
```
- Laravel
```php
$data = DB::select("SELECT kilometer FROM tyres WHERE usage=1 ORDER by id DESC LIMIT 1");

Tyres::select('kilometer')->where('usage',1)->orderBy('id', 'DESC')->take(1)->get();
```

#
#### Laravel Add Request
```php
$request->merge(['a' => 1]);
```
```json
{
    "a" : "1"
}
```

#
#### Laravel bcrypt Encript
```
$data->password = bcrypt($r->password);
```

#
#### PhpMyAdmin Time Zone
```
SET time_zone ='+08:00';
```

#
#### Laravel Time Zone

- AppServiceProvider.php
```php
<?php

namespace App\Providers;

use Carbon\Carbon;
use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider
{

    ...

    public function boot()
    {
        config(['app.locale' => 'id']);
        Carbon::setLocale('id');
        date_default_timezone_set('Asia/Jakarta');
    }
}
```

- app.php
```php
<?php

use Illuminate\Support\Facades\Facade;

return [

    ...

    'timezone' => 'Asia/Jakarta',

    'locale' => 'id',

    'fallback_locale' => 'id',

    'faker_locale' => 'id_ID',

    ...
];
```

#
#### Html input number decimal
```php
<input step="any"/>
```

#
#### Html
```php
<input tabIndex="-1"/>
```

#
#### Ajax URL
```js
url: "{{ route('products.data') }}",
```
```js
url: "/products/data",
```
```js
var base_url = window.location.origin;
//localhost:8000
var url = base_url + "/penyulang/byidgi/" + id;

$.ajax({
    url: url,
});
```

#
#### HTML TABLE TD WRAPCONTENT
```html
<td style="width: 1px; white-space: nowrap;">{{$d->updated_at}}</td>
```

#
#### Update join table
```sql
UPDATE trans_product_out SET price = ( SELECT price FROM products WHERE trans_product_out.products_id = products.id );
```

#
#### Max + 1
```php
'order_no' => MenuHeadersModel::max('order_no') + 1
```

#
#### HTML Table Horizontal Scroll
```html
<style>
 .table_wrapper{
    display: block;
    overflow-x: auto;
    white-space: nowrap;
}
</style>

<div class="table_wrapper">
<table>
...
</table>
</div>
```

#
#### Php Combine Array
```php
$a = [
    'a' => 1,
    'b' => 2,
];
$b = [
    'c' => 3,
    'd' => 4,
];
$sent = array_merge($a, $b);

//become
$sent = [
    'a' => 1,
    'b' => 2,
    'c' => 3,
    'd' => 4,
];
```

#
#### Auto Col Size

[Source](https://www.w3schools.com/bootstrap/bootstrap_grid_examples.asp)

```html
<div class="row row-cards">
  @foreach($params as $d)
  <div class="col-sm-6 col-lg-4">
    <div class="form-group">
      <label for="name">Name</label>
      <input type="text" class="form-control" id="name[]" name="name[]" placeholder="" required>
    </div>
  </div>
  @endforeach
</div>
```

#
#### Select Readonly Not Disabled

```html
<input disabled/>
```
```html
<input style="pointer-events: none; background-color: #fafbfc;"/>
```

#
#### PHP A To ZZ
```php
function excelColumnRange($lower, $upper) {
    ++$upper;
    for ($i = $lower; $i !== $upper; ++$i) {
        yield $i;
    }
}

foreach (excelColumnRange('A', 'ZZ') as $value) {
    echo $value, PHP_EOL;
}
```

#
#### Laravel Border Excel

[Source](https://docs.laravel-excel.com/2.1/reference-guide/borders.html)

#
#### MySqlBackUp

[Source](https://stackoverflow.com/questions/18022809/how-to-solve-error-mysql-shutdown-unexpectedly)

|<img src="/preview/preview1.png" width="300"/>|
|--|

#
#### Route 404 Laravel
```
composer install
```
```
php artisan route:clear
```
```
php artisan route:cache
```

#
#### Redirect
```php
->name('login');
return redirect()->to('login');
```

#
#### Datatables Render
```js
render: function(data, type, row) {
    if (data == null) {
        return '-';
    }
    return data;
}
```

#
#### Flash Message
```html
  <div class="row">
    @if(session('sukses'))
    <div class="alert alert-success" role="alert">
      {{session('sukses')}}
    </div>
    @endif
  </div>
```
```php
return redirect('/products')->with('sukses', 'Data successfully added');
```

#
#### Web HTML ADD ITEM INSIDE DIV
```js
document.getElementById('gardu_photo').appendChild(element);
```
```js
<html>
<head>

<script>

function test() {
    var element = document.createElement("div");
    element.appendChild(document.createTextNode('The man who mistook his wife for a hat'));
    document.getElementById('lc').appendChild(element);
}

</script>

</head>
<body>
<input id="filter" type="text" placeholder="Enter your filter text here.." onkeyup = "test()" />

<div id="lc" style="background: blue; height: 150px; width: 150px;" onclick="test();">
</div>
</body>

</html>
```
```js
var div = document.getElementById('divID');

div.innerHTML += '<p></p>';
```

#
#### Foreach Loop
```html
@forEach($data as $d)
    {{$loop->iteration}}
@endforeach
```

#
#### ARRAY TO OBJECT
```
json_decode (json_encode ($var), FALSE);
```

#
#### Js Find Html
```
Route::get('/counttransaction', [HomeController::class, 'countTransaction']);
```
```
public function countTransaction()
{
    $date = date("Y-m");
    $data = DB::select('select count(id) as count from m_products where created_at like "%' . $date . '%";')[0];
    return $data;
}
```
```
function profitSales() {

    $.ajax({
        url: '/home/profitsales',
        type: "GET",
        dataType: "JSON",
        success: function(data) {
            document.getElementById('profitSales').innerHTML = "Rp. " + (data.count.toLocaleString());
        },
        error: function(jqXHR, textStatus, errorThrown) {}
    });
}
```

#
#### Select to Array 1D
```
DB::table('models')->where('id', '>', 0)->pluck('id')->toArray();
```
```
Models::where('id', '>', 0)->lists('id')->toArray();
```
```
[1,2,3,4,5,6]
```

#
#### Bootstrap CSS JS
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.1.3/dist/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.1.3/dist/js/bootstrap.min.js" integrity="sha384-ChfqqxuZUCnJSK3+MXmPNIyE6ZbWh2IMqE241rYiqJxyMiZ6OW/JmZQ5stwEULTy" crossorigin="anonymous"></script>
<script src="https://code.jquery.com/jquery-3.3.1.js" integrity="sha256-2Kok7MbOyxpgUVvAk/HJ2jigOSYS2auK4Pfzbm7uH60=" crossorigin="anonymous"></script>
```
```html
<link rel="stylesheet" href="https://cdn.datatables.net/1.11.5/css/dataTables.bootstrap4.min.css" />
<link rel="stylesheet" href="https://cdn.datatables.net/rowreorder/1.2.8/css/rowReorder.bootstrap4.min.css" />

<script src="https://code.jquery.com/jquery-3.5.1.js"></script>
<script src="https://cdn.datatables.net/1.11.5/js/jquery.dataTables.min.js"></script>
<script src="https://cdn.datatables.net/1.11.5/js/dataTables.bootstrap4.min.js"></script>
<script src="https://netdna.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>
<script src="https://cdn.datatables.net/rowreorder/1.2.8/js/dataTables.rowReorder.min.js"></script>
```

#
#### Url Decode
```
urldecode($r->name);
```

#
#### JS Response
```
function myItemNameSearch(Request $r)
{
   $tanggal = $r->tanggal;
    return response(['tanggal'=>$tanggal]);
}
```

#
#### VSCode Visual Studio Code Format Code

|<img src="/preview/preview2.png" width="300"/>|
|--|

#
#### JQUERY
```
<script src="https://code.jquery.com/jquery-3.5.1.js"></script>
```


---

```
Copyright 2022 M. Fadli Zein
```