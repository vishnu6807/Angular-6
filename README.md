# Angular-6

Attribute and propety of Html elemtent are two different things
We could change property of Html element but cant change the value

Interpolation and Property binding are almost similar but only differnce is this 
to change certain propety like disabled interploation does not work so we need to 
use Propery binding
<input id=xyz disabled="true/false">  --not work
<input id=xyz [disabled]="true/false">  --work

<input id=xyz [disabled]="propertyinclass">  --work
class component{
propertyinclass="true"
}

class binding
it is similar to bind particular css class to our html elements
<h1 class="myclass" [class]="anotherclass">
In this way properties of  myclass will be override by  anotherclass (little bit similar of  important flag in css)

we could use different classees based on value of paticular varible
<h1 class.myclass="variable">
variable=true/false

we could use different classees based on of value of  particular variable in an array
<h1 [ngClass]="array">

array{
variable=true/false
variable2=true/false
}


style binding 
<h2 style="color:blue"  [style.color]="'red'">hii vehicle</h2>
in this example [] will override style 

we could also use object in compont class to give values to ngStyle 
<h2   [ngStyle]="object">hii vehicle</h2>

Event Handling vs Data handing
Conttrolling data from class to Template –Data Handling
Conttrolling  data from Template to class based on event –Event Handling



Click event 
 <button (click)="welcomeFunction()">welcome msg</button>
public msg="";

welcomeFunction()
  {
  	this.msg="Hi vishnu welcome to Angular 6" //this is imp
  } 

$event –we could pass this to function call as parameter to get detailed info on onging event

to set variable to particular value using onclick

<button (click)="msg='kkk'">welcome msg</button>
   <h2> {{msg}}</h2>

 Reference var like ng-model
 to take input from text box and send on onclick
   <input #refvar_for_input type="text"> //# tag before variable name
   <button (click)="modelFuction(refvar_for_input.value)">welcome msg</button>

two way binding 

import {FormsModule} from '@angular/forms'; //in app module
add FormsModule to the import module

<div>
   <h3> two way binding using ngModel</h3>
   <input [(ngModel)]=textbox type="text">
   <h2> {{textbox}}</h2>
  
   </div>

if else blocks
<h3> if else blocks in angular</h3>

   <div *ngIf= "condition_Var then ifblock; else elseblock"> </div>
   
 <ng-template #ifblock>
 <h3>inside if block</h3>
  </ng-template>

  <ng-template #elseblock>
 <h3>inside else block</h3>
  </ng-template>

   </div>

Switch case
<div [ngSwitch]="code"> 
   <div *ngSwitchCase="'one'">First Use case</div>
   <div *ngSwitchCase="'two'">Second Use case</div>
   <div *ngSwitchCase="'three'">Thrid Use case</div>
<div *ngSwitchDefault>Nothing has given</div>
   
</div>



 Component  interaction

 <app-child [parentData]="name"></app-child>
@Input () public parentData;


Service creation 
command 
 ng g s service_name
ng g s myservice

import  MyserviceService class into component
inject it into constuctor of components 

constructor(private _myservice :MyserviceService) { }

call the required method from service

  ngOnInit() {
  	this.teamMates=this. _myservice.GetmyTeammates();
  }


Routing 
command 
ng new project –routing

create new components.

Import those components in app-routing moule file
 Add those components to route array in app-routing moule file

const routes: Routes = [
{path:'url_',component:component name},
{path:'employees',component:EmployeesComponent }
];


better if we export those comoponents  into an array and use this array in app.module
in components so that there will only one compopoent for all routing components 

Wildcard Route
if some url is not present and user hits the same then it throws error in the console
there should be page like showing msg page not found

create new component and add add proper msg on html page

add this as a last entry in route array in app-routing module file remember it should be last entry
othrwise for any url this page will appear

{path:"**",component:PageNotFoundComponent }

add the same component in export array

this is to make redirect to default url when the url provided is null i.e localhost:4200

{path:'',redirectTo:'_url',pathMatch:'full'},

Passing parameters while routing 

it is case when thre is need to pass paramerters while  routing and we can use this paramer in bussiness logic 

create list object  and itetate using for loop

create component 2 need to display when click on some list 

add it into route array

{path:'_url/:id',component:component_name_2}

call function onClick (any event ) on list

<li (click)="onClickProject(x)">

import router to navigate between url to pass parameter
import { Router} from '@angular/router';

onClickProject(parameter)
  	{
  		this._router.navigate(['/url',parameter .id]);
  	}

it will show paramter passed in url 

to access this parameter into our  component_name_2

import { ActivatedRoute} from '@angular/router';
and inject it into constructor and use this method into oninit()

let id=parseInt(this._route.snapshot.paramMap.get('id'));
 
declare id into class and assign id to it
display the same using interpolation

ParamMap observable

angular does not intilise the component when url changes(id in our case)
so from previous 
let id=parseInt(this._route.snapshot.paramMap.get('id'));
id changes in the url but on html (interpolation) it does not change
so we need to subscribe to paramMap


this._route.paramMap.subscribe(()=>{
      /*let id= this.id;*/
      this.project_id= +this._route.snapshot.paramMap.get('id');
 });


Go back one url using browser functionality 

import location 
import { Location } from '@angular/common';

inject dependancy for the same

goBack(): void {
  this.location.back();
}

<button (click)="goBack()">go back Using browser func</button>

(ngModelChange)—used in select dropdown list in order to call function

ng update @angular/cli @angular/core
to update version of angular 

