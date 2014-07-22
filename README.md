vFramework
==========

framework for AngularJS Client VSOFT


==========

#Get Started



(1) Get vFramework in one of 4 ways:

* clone & build this repository
* via Bower: by running $ bower install angular-collection console

(2) Include vsoft.js (or vsoft.min.js) in your index.html, after including Angular itself (For Component users: ignore this step)

(3) Include Config.js in your index.html

(4) Add 'vFramework' to your main module's list of dependencies 

####When you're done, your setup should look similar to the following:

==========

```html
<script src="bower_components/angular-collection/angular-collection.min.js"></script>

<script src="scripts/Config.js"></script>
<script src="scripts/vsoft.js"></script>
```

```javascript
angular.module('yourApp', [
    'vFramework'  
])
```

##Using vFramework


 ```javascript
 deviceID : {String} // mã ID của thiết bị 
 defaultPass : {String}  //pass của thiết bị || null
 apiHost : {String}  //địa chỉ hosting // apiHost : 'http://itaxi.vn'
 mediaHost : {String} // địa chỉ media hosting
 disableLog: {
            info: true, // true : tắt chức năng logger.info
            error: false, // false : Hiển thị
            debug: false
    }
 loginRouteServer: {String}, // server node.js route /login
 logoutRouterServer: {String},// server node.js route /logout
 registerRouterServer: {String},// server node.js route /register
 loginTableName: {String} // table name login users
 
  ```
==========

##Cấu hình roles :
 
 
####Xây dựng danh sách tất các các Roles bạn sử dụng trong App :
 
  ```javascript
 roles: [
     'anon',
     'user'
 ]
  ```
 
 
#### Thiết lập tất cả các quyền truy cập mà bạn định ngĩa theo từng cấp độ sử dụng
 
  ```javascript
 accessLevels: {
      'anon': ['anon'],
      'user': ['user']
 }
  ```
  
####Export roles
  
  ```javascript
 exports.userCan =
 {
     accessUser: exports.accessLevels.user // Export 1 roles 'user'
 };
  ```
  File app.js khai báo trong State quyền truy cập cao nhất mà roles đó có thể thực hiện
```
 accessLevel: window.userCan.accessUser
```
#####Example
 ```javascript
 .state('main.home', {
                url: "",
                templateUrl: 'views/states/home.html',
                controller: 'homeCtrl',
                accessLevel: window.userCan.accessUser // Quyền User sẽ được truy cập
            })
 ```
 
### Using Service

Param         |        Types | description
------------- | ------------- | ----------
TableName   |  String   | Tên bảng dữ liệu cần lấy
rStart  |      Numbe    | Start Lấy phần tử từ vị trí || để null mặc định 0
 Limit |       Number   | Tối đa phần tử được lấy || để null mặc định 1000
 Filters   |    Array   | Lọc theo điều kiện || null
 Sorters  |    Array    | Sắp xếp || null

         

#####example
         
```javascript
          var sorters = [{property: 'startAt', direction: 'DESC'}];`
```
        
```javascript
         $fetchData.getData('users', null, null, null, null).then(function (resp) {
                console.log('data Users : '), resp.all();

             }, function (err) {
                console.log('err : ', err);
         })
```

#####Example  

```javascript
         var filters = [
         {
             property: 'driver', // thuộc tính Driver
             value: userId, // lọc lấy theo ID
             type: 'string',
             comparison: 'eq' // so sánh bằng...
         }
         ];

         var sorters = [
         {
             property: 'startAt', // sắp xếp theo ngày bắt đầu - đây là 1 kiểu thời gian
             direction: 'DESC' // kiểu sắp xếp
         }
         ];

         $fetchData.getData('RouteHistories', null, null, filters, sorters).then(function (resp) {
                console.log('RouteHistories', $scope.RouteHistories);
            }, function (err) {
                console.log('err : ', err);
            })
```
         

#####Lấy dữ liệu từ service


Param         |        Types | description
------------- | ------------- | ----------
TableName   |  String   | Tên bảng cần lấy dữ liệu
Id  |      String    | Id của đối tượng cần lấy
 NameStorage |       String   | NameStorage dataStorage truyền vào || null (để null sẽ lấy từ server)


         
         ```javascript
         $fetchData.getDataId('UserAuths', '5397ca5dc0c8174642000001').then(function(resp){
                console.log('data : ',resp);
                },function(err){
                console.log('err :',err);
         });
         ```
         

