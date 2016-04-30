---
layout: post
title:  "AngularJS list item options with ng-repeat,ng-class,ng-click,ng-mouseover,ng-mouseleave etc!"
date:   2016-04-25 13:18:23
categories: mytags update
tags: [mytags]
---
HTML is great for declaring static documents, but it falters when we try to use it for declaring dynamic views in web-applications. `AngularJS` lets you extend HTML vocabulary for your application. The resulting environment is extraordinarily expressive, readable, and quick to develop. 

### AngularJS stylish list item

### 1. CSS

{% highlight ruby %}
*{
	margin:0;padding:0;
	}
body{
	background:#E7E19C;
	font-family:Constantia, "Lucida Bright", "DejaVu Serif", Georgia, serif;
	}	
#main_wrap{
	width:1024px;
	min-height:1000px;
	background:#fff;
	margin:0 auto;
	padding-top:2px;
	}	
	

ul.options{
	list-style:none;
	margin:20px;
	}	
ul.options li{
	display:inline-block;
	border:3px solid #ddd;
	background:#fafafa;
	cursor:pointer;
	font-size:20px;
	position:relative;
	color:#000;
	width:100px;
	height:50px;
	line-height:50px;
	text-align:center;
	-webkit-transition:all  0.3s  ease 0s;
         -moz-transition:all  0.3s  ease 0s;
               -o-transition:all  0.3s  ease 0s;
                     transition:all  0.3s  ease 0s;
	}	
ul.options li span.tick{
	position:absolute;
	right:0;
	top:0;
	
	font-size:14px;
	line-height:20px;
	color:#999;
	width: 0;
height: 0;
border-style: solid;
border-width: 0 30px 30px 0;
border-color: transparent #ddd transparent transparent;
	/*-ms-transform-origin: 50% 50%;
  -webkit-transform-origin: 50% 50%;
  -moz-transform-origin: 50% 50%;
  transform-origin: 50% 50%;
  transform: rotate(90deg);
  -moz-transform: rotate(90deg);
  -webkit-transform: rotate(90deg);
  -o-transform: rotate(90deg);
  -ms-transform: rotate(90deg);*/
	}	
ul.options li span.tick i{position:absolute;left:14px;}	
ul.options li.notavailable{
	background:#ddd;
	color:#999;
	cursor:default;
	}	
ul.options li.notavailable 	span.tick{display:none;}
ul.options li.onhover{
	border:3px solid #999;	
	}	
ul.options li.onhover span.tick{
	display:block;
	border-color: transparent #999 transparent transparent;
	color:#fff;
	}	
ul.options li.selected{
	border:3px solid #0080FF;	

	}		
ul.options li.selected span.tick{
	display:block;
	border-color: transparent #0080FF transparent transparent;
	color:#fff;
	}	
	
	
ul.options_identify{
	list-style:none;
	margin:20px;
	}	
ul.options_identify li{
	display:block;
	border:1px solid #ddd;
	}	
		
ul.options_identify li span.icon{
	width:100px;
	height:50px;
	line-height:50px;
	border:3px solid #ddd;
	display:inline-block;
	position:relative;
	}
ul.options_identify li span.icon span.tick{
	position:absolute;
	right:0;
	top:0;
	
	font-size:14px;
	line-height:20px;
	color:#999;
	width: 0;
height: 0;
border-style: solid;
border-width: 0 30px 30px 0;
border-color: transparent #ddd transparent transparent;
	
	}	
ul.options_identify li span.icon span.tick i{position:absolute;left:14px;}				
ul.options_identify li span.icon.nottouse{
	background:#ddd;
	}	
ul.options_identify li span.icon.youchoose{
	border:3px solid #0080FF;	

	}		
ul.options_identify li span.icon.youchoose span.tick{
	display:block;
	border-color: transparent #0080FF transparent transparent;
	color:#fff;
	}	
ul.options_identify li span.text{
	display:inline-block;
	vertical-align:top;margin-left:5px;
	position:relative;
	}		
{% endhighlight %}

### 2. HTML 

{% highlight ruby %}
 
 <!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>Selected Options</title>
<link rel="stylesheet" type="text/css" href="style.css"/>
<link rel="stylesheet" type="text/css" href="font-awesome.css"/>
<script src = "https://ajax.googleapis.com/ajax/libs/angularjs/1.3.3/angular.min.js"></script>
<script src="myscript.js"></script>

</head>

<body>
 <div id="main_wrap" ng-app = "mainApp">
 <div ng-controller = "optionsController">
   <ul class="options" >
     <li 
     ng-class="{onhover: hovering && $index != notavailableindex,selected: ($index == selectedindex && $index != notavailableindex),notavailable: $index == notavailableindex}"  
     ng-mouseover="hovering = true"
     ng-mouseout="hovering = false" 
     ng-click="($index == notavailableindex) || show($index); ($index == notavailableindex) || addclass($index);" 
     data-val="{{option.product_name}}" 
     ng-repeat="option in lioptions.liitems"
     >
     <span>{{option.product_name}}</span><span class="tick"><i class="fa fa-check"></i></span>
     
     </li>
     
   </ul>
   <input type="hidden" name="hidDataval" id="hidDataval"/>
   <div style="margin:5px;">Selected Option is : <span class="opt">{{lioptions.currentitem}}</span></div>
   
 </div>  
   
    
 <ul class="options_identify">
   <li><span class="icon nottouse"></span><span class="text">Already Taken</span></li>
   <li><span class="icon"><span class="tick"><i class="fa fa-check"></i></span></span><span class="text">Available</span></li>
   <li><span class="icon youchoose"><span class="tick"><i class="fa fa-check"></i></span></span><span class="text">You choose</span></li>
 </ul>
   
 </div>
 
 

 
</body>
</html>


{% endhighlight %}


### 3. myscript.js

{% highlight ruby %}
<script>
      var mainApp = angular.module("mainApp", []);

      mainApp.controller('optionsController', function ($scope) {
      $scope.lioptions = {
		  
		     liitems:[
	                 { product_name: "Product 1",price: 20},
			         { product_name: "Product 2",price: 50},
					 { product_name: "Product 3",price: 40},
					 { product_name: "Product 4",price: 60},
					 { product_name: "Product 5",price: 45},
					 { product_name: "Product 6",price: 345},
					 { product_name: "Product 7",price: 455}
	                   		 
			 ],
			 
			 currentitem:''
			 
			
	  };
			 $scope.show = function(index) {
               //$scope.items.splice(index, 1);
			   var obj;
               obj = $scope.lioptions;
			   //if($scope.notavailableindex !=index)	
			   obj.currentitem= "Product - "+obj.liitems[index].product_name +" Price - "+obj.liitems[index].price;
			   //$scope.selectedindex=index;
             } 
			 
			 $scope.addclass = function(index) {
               //$scope.items.splice(index, 1);
			   var obj;
               obj = $scope.lioptions;	
			  // if($scope.notavailableindex !=index)		 
			   $scope.selectedindex=index;
			  // alert($scope.selected);
             } 
			 
			 $scope.selectedindex = null;
			 $scope.notavailableindex = 2;
			 
             });

          </script>
     {% endhighlight %}     
