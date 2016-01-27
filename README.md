# ng2-interfaces

Welcome to the ng2-interfaces wiki!

## How do I use interfaces better on typescript with ng2?

### 1st step
Using the [Angular2 Quick Start](https://angular.io/docs/ts/latest/quickstart.html) you will have your environment ready to proceed the next steps.

### boot.ts
Edit your boot file to have the code bellow


<html>
<head>
    <title>Boot.ts</title>

    <script>
        import {bootstrap} from 'angular2/platform/browser'
        import {bind, Inject, Injectable} from 'angular2/core'
        
        interface MyServiceInterface {
           getName: () => String;
        }
        
        class MyService implements MyServiceInterface {
           getName() {
              return 'Dan';
           }
        }

        class MyServiceJordan implements MyServiceInterface {
           getName() {
              return 'Jordan';
           }
        }

        var serviceInjector = bind('myAliasService').toClass(MyService);
        //var serviceInjector = bind('myAliasService').toClass(MyServiceJordan);
        
        
        
        @Component({
           selector: 'hello',
           template: 'Hello world, {{ name }}',
           providers:[serviceInjector]
        }) class HelloComponent {
           name: String;
           constructor(@Inject('myAliasService') private _service: MyServiceInterface){
              this.name = _service.getName();
           }   
        }
        
        bootstrap(HelloComponent)
    </script>

</head>
<body>
    
</body>

</html>


### index.html
For your index.html replace for it.

<html>
<head>
    <title>Angular 2 QuickStart</title>

    <!-- 1. Load libraries -->
    <script src="node_modules/angular2/bundles/angular2-polyfills.js"></script>
    <script src="node_modules/systemjs/dist/system.src.js"></script>
    <script src="node_modules/rxjs/bundles/Rx.js"></script>
    <script src="node_modules/angular2/bundles/angular2.dev.js"></script>

    <!-- 2. Configure SystemJS -->
    <script>
        System.config({
        packages: {        
          app: {
            format: 'register',
            defaultExtension: 'js'
          }
        }
      });
      System.import('app/boot')
            .then(null, console.error.bind(console));
    </script>

</head>
<body>
    <hello></hello>
</body>

</html>


## Understanding what has happened...

Mostly the examples provided by angular.io and people in the community regarding DI, it is using the concrete class. But with Typescript, we can take advantage of using interfaces. When you define an interface you are setting up a protocol between 2 or more parts in a system/webapp/mobapp/whateverapp. The main advantage of it is that you can change your concrete class for another one and the effort to do it consist in changing your concrete class and the mapping (bind to create an injector). Thus, you can see that you won't need to change all the other parts of your whateverapp adapting to the new implementation.

You can try just changing the injector commented

        
            //var serviceInjector = bind('myAliasService').toClass(MyService);
            var serviceInjector = bind('myAliasService').toClass(MyServiceJordan);



I hope it helps someone else.


What I most love is breaking walls to make development easier. ;)
Please, feedback with critics and reviews. 
