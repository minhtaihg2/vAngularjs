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

#Using vFramework

 ```
 
 deviceID : {String}  mã ID của thiết bị //
 defaultPass : {String}  pass của thiết bị || null
 apiHost : {String}  địa chỉ hosting // apiHost : 'http://itaxi.vn'
 mediaHost : {String}  địa chỉ media hosting
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
  
 #Cấu hình roles :
 
 
 ###Xây dựng danh sách tất các các Roles bạn sử dụng trong App :
 
  ```html
 roles: [
 'anon',
 'user'
 ]
 
  ```
 
 
### Thiết lập tất cả các quyền truy cập mà bạn định ngĩa theo từng cấp độ sử dụng
 
  ```html
 accessLevels: {
      'anon': ['anon'],
      'user': ['user']
 }
  ```
  
  ###Export roles
  
  ```
 exports.userCan =
 {
     accessUser: exports.accessLevels.user // Export 1 roles 'user'
 };
  ```
  File app.js khai báo trong State quyền truy cập cao nhất mà roles đó có thể thực hiện
```
 accessLevel: window.userCan.accessUser
```
 Example
 ```html
 .state('main.home', {
                url: "",
                templateUrl: 'views/states/home.html',
                controller: 'homeCtrl',
                accessLevel: window.userCan.accessUser // Quyền User sẽ được truy cập
            })
 ```

