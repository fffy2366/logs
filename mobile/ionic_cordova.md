# 使用Ionic + Apache Cordova开发跨平台混合型的移动应用
转自：http://blog.csdn.net/zoutongyuan/article/details/41910903?utm_source=tuicool
JavaScript 写多了，要想真正提高js水平，研究其他js框架源码是不错的选择。Github上大部分都是js、css相关的项目，可以有目的性的 check out 下来，研读研读，还是非常收益的，跟随nb的人，也会慢慢变的nb。

场景：有一个朋友，他公司是做移动应用开发的，3个安卓开发人员，3个 iOS，然后是 Java 开发，美工 ，10多个人的公司，主要是以接项目为主，一个项目（电商、微信、聊天 类型的）大概在20万左右， 差不多1个半月 做完（代码质量能不能保证，不知道，不过我觉得开发是一件很严谨的事，要开发出高性能、高健壮性的程序，还是很难的），公司销售很给力，能谈下好几个项目。问题来了，要能同时进行好几个项目，就要招 移动开发的人，如果有时没接到项目，那 ，又会闲着。如果有些 客户 要 做 wp ，黑莓的 ，那就做不来了。于是迫切 想 找一些跨平台的 开发技术 来 解决问题？

这个场景是真实的，不是 yy，那么我们来玩玩 Ionic ，Apache Cordova 这些技术，这样我们就有更深入的 理解了。
我做过 一些 安卓的小东西，ios 没玩过；我是一个  web技术 狂热者，很看好web技术；我认为那些 Android 、ios 等等  将会慢慢 被 web 技术 取代，浏览器 作为跨平台的中间件，将会成为主流。do not mind

尊重原创，转载请注明出去：http://blog.csdn.net/zoutongyuan/article/details/41910903

进入主题吧。
1、Ionic 是什么？
好吧，我们看 Ionic 能给我们提供什么?  一个样式库，你可以使用它 来 装饰你的 HTML 网页 ，看起来 想 移动程序的 界面，什么 header 、content、footer、grid、list。这貌似没什么 实质性的东西， sencha touch ，jq 都能提供 。
一个用 AngularJS 写的 工具库，姑且叫它 组件库吧。Ionic的 grid 设计的比较合理，比 bootstrap的 更强大。
当然它 还包含 了angular-animate、angular-resource、angular-sanitize、angular-ui-router，适应移动平台的模块库。

2、Apache Cordova 是什么？
Apache Cordova 提供用 Javascript 访问 移动平台  的 API 。
其内部是用每个 平台下的  web view 组件，运行 程序，然后实现了 每个平台下的 一套 CordovaLib  供你写的程序调用，然后你就可以 调用 摄像头、磁盘等 重api。

接下来 动手玩玩。首先安装nodejs，和平台的 （ios || android）sdk，这里不在 累述 
1、先安装 cordova
npm install -g cordova
2、安装 Ionic
npm install -g ionic

3、创建项目
ionic start todo blank

4、配置平台
ionic platform add android

然后 在IDE中打开 项目：


www是主目录
index.html 是 主页面

刚才我们配置 平台的时候 ，工具帮我们做了一件事，创建 了一个 安卓 应用，
创建一个 CordovaApp 类，继承自 CordovaActivity ， Activity 是 安卓的4大组件，表示可以看到 了一块窗口。
它做了一个 引导，就是loadUrl，这里不做过多的 介绍，有兴趣 我们以后深入研究，这里我们只是 发散性的引导。

现在，你就可以使用 ionic 和 Apache Cordova 提供的 api 来 开发 跨平台的应用了。

来改我们的inde.html
[html] view plain copy print?在CODE上查看代码片派生到我的代码片
<!DOCTYPE html>  
<html>  
<head>  
    <meta charset="utf-8">  
    <meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no, width=device-width">  
    <title></title>  
  
    <link href="lib/ionic/css/ionic.css" rel="stylesheet">  
    <link href="css/style.css" rel="stylesheet">  
  
    <!-- IF using Sass (run gulp sass first), then uncomment below and remove the CSS includes above  
    <link href="css/ionic.app.css" rel="stylesheet">  
    -->  
  
    <!-- ionic/angularjs js -->  
    <script src="lib/ionic/js/ionic.bundle.js"></script>  
  
    <!-- cordova script (this will be a 404 during development) -->  
    <script src="cordova.js"></script>  
  
    <!-- your app's js -->  
    <script src="js/app.js"></script>  
</head>  
<body ng-app="todoApp" ng-controller="TodoController" ng-cloak>  
  
    <ion-side-menus>  
  
        <!-- Center content -->  
        <ion-side-menu-content>  
            <ion-header-bar class="bar-dark">  
                <button class="button button-icon" ng-click="toggleProjects()">  
                    <i class="icon ion-navicon"></i>  
                </button>  
                <h1 class="title">{{activeProject.title}}</h1>  
                <!-- New Task button-->  
                <button class="button button-icon" ng-click="newTask()">  
                    <i class="icon ion-compose"></i>  
                </button>  
            </ion-header-bar>  
            <ion-content scroll="false">  
                <ion-list>  
                    <ion-item ng-repeat="task in activeProject.tasks">  
                        {{task.title}}  
                    </ion-item>  
                </ion-list>  
            </ion-content>  
        </ion-side-menu-content>  
  
        <!-- Left menu -->  
        <ion-side-menu side="left">  
            <ion-header-bar class="bar-dark">  
                <h1 class="title">Projects</h1>  
                <button class="button button-icon ion-plus" ng-click="newProject()">  
                </button>  
            </ion-header-bar>  
            <ion-content scroll="false">  
                <ion-list>  
                    <ion-item ng-repeat="project in projects" ng-click="selectProject(project, $index)" ng-class="{active: activeProject == project}">  
                        {{project.title}}  
                    </ion-item>  
                </ion-list>  
            </ion-content>  
        </ion-side-menu>  
  
    </ion-side-menus>  
  
    <script id="new-task.html" type="text/ng-template">  
        <div class="modal">  
  
            <!-- Modal header bar -->  
            <ion-header-bar class="bar-secondary">  
                <h1 class="title">New Task</h1>  
                <button class="button button-clear button-positive" ng-click="closeNewTask()">Cancel</button>  
            </ion-header-bar>  
  
            <!-- Modal content area -->  
            <ion-content>  
  
                <form ng-submit="createTask(task)">  
                    <div class="list">  
                        <label class="item item-input">  
                            <input type="text" placeholder="What do you need to do?" autofocus ng-model="task.title">  
                        </label>  
                    </div>  
                    <div class="padding">  
                        <button type="submit" class="button button-block button-positive">Create Task</button>  
                    </div>  
                </form>  
  
            </ion-content>  
        </div>  
    </script>  
  
</body>  
</html>  

js/app.js
[javascript] view plain copy print?在CODE上查看代码片派生到我的代码片
var todoApp = angular.module('todoApp', ['ionic']);  
  
todoApp.run(function ($ionicPlatform) {  
    $ionicPlatform.ready(function () {  
        if (window.cordova && window.cordova.plugins.Keyboard) {  
            cordova.plugins.Keyboard.hideKeyboardAccessoryBar(true);  
        }  
        if (window.StatusBar) {  
            StatusBar.styleDefault();  
        }  
    });  
});  
  
  
todoApp.controller('TodoController', function ($scope, $timeout, $ionicModal, Projects, $ionicSideMenuDelegate) {  
  
    // A utility function for creating a new project  
    // with the given projectTitle  
    var createProject = function (projectTitle) {  
        var newProject = Projects.newProject(projectTitle);  
        $scope.projects.push(newProject);  
        Projects.save($scope.projects);  
        $scope.selectProject(newProject, $scope.projects.length - 1);  
    }  
  
  
    // Load or initialize projects  
    $scope.projects = Projects.all();  
  
    // Grab the last active, or the first project  
    $scope.activeProject = $scope.projects[Projects.getLastActiveIndex()];  
  
    // Called to create a new project  
    $scope.newProject = function () {  
        var projectTitle = prompt('Project name');  
        if (projectTitle) {  
            createProject(projectTitle);  
        }  
    };  
  
    // Called to select the given project  
    $scope.selectProject = function (project, index) {  
        $scope.activeProject = project;  
        Projects.setLastActiveIndex(index);  
        $ionicSideMenuDelegate.toggleLeft(false);  
    };  
  
    // Create our modal  
    $ionicModal.fromTemplateUrl('new-task.html', function (modal) {  
        $scope.taskModal = modal;  
    }, {  
        scope: $scope  
    });  
  
    $scope.createTask = function (task) {  
        if (!$scope.activeProject || !task) {  
            return;  
        }  
        $scope.activeProject.tasks.push({  
            title: task.title  
        });  
        $scope.taskModal.hide();  
  
        // Inefficient, but save all the projects  
        Projects.save($scope.projects);  
  
        task.title = "";  
    };  
  
    $scope.newTask = function () {  
        $scope.taskModal.show();  
    };  
  
    $scope.closeNewTask = function () {  
        $scope.taskModal.hide();  
    }  
  
    $scope.toggleProjects = function () {  
        $ionicSideMenuDelegate.toggleLeft();  
    };  
  
  
    // Try to create the first project, make sure to defer  
    // this by using $timeout so everything is initialized  
    // properly  
    $timeout(function () {  
        if ($scope.projects.length == 0) {  
            while (true) {  
                var projectTitle = prompt('Your first project title:');  
                if (projectTitle) {  
                    createProject(projectTitle);  
                    break;  
                }  
            }  
        }  
    });  
  
});  
  
  
todoApp.factory('Projects', function () {  
    return {  
        all: function () {  
            var projectString = window.localStorage['projects'];  
            if (projectString) {  
                return angular.fromJson(projectString);  
            }  
            return [];  
        },  
        save: function (projects) {  
            window.localStorage['projects'] = angular.toJson(projects);  
        },  
        newProject: function (projectTitle) {  
            // Add a new project  
            return {  
                title: projectTitle,  
                tasks: []  
            };  
        },  
        getLastActiveIndex: function () {  
            return parseInt(window.localStorage['lastActiveProject']) || 0;  
        },  
        setLastActiveIndex: function (index) {  
            window.localStorage['lastActiveProject'] = index;  
        }  
    }  
})  

这个todo 我们没有用到 Apache Cordova 的api，所以，这个项目在浏览器中 也可以运行。
使用 
$ ionic serve


在我的小米3 中 看看。使用下面命令，你可能要安装好 驱动，
$ ionic run android


最后编译，
$ cordova build --release android

来评价这一些技术吧。
天下大势，合久必分，分久必合。
HTML5 + CSS3 + Javascript 最适合作为跨平台的技术栈，其开放 ，自由，每个人都可以 为这些技术的制定 ，发表意见 ，像 使用 svg 、canvas 、css 3动画 开发的游戏  ，已经在撼动 桌游， 手游 等 原生语言开发的 应用了，所以不仅仅是 应用。
而 Apache Cordova  只是 一个 过渡阶段的产物。对于 新技术的 出现 ，是值得鼓励的 。
让我们拭目以待，web 技术 明天的发展吧。
