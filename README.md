# Running-multiple-time-request-in-postman
#this is code is for running multiple request in postman using variables
#you have to add scripts in body, pre-request and test sections 

#body section : define a variable 
{
"hasmanager":"manager"
}

#pre-request section: create an array and add values you want to run 

var managers= pm.environment.get("managers");

if(!managers){
     managers=[0,1];
  ;
     
}

var currentmanager=managers.shift();
pm.environment.set("manager",currentmanager);
pm.environment.set("managers",managers) ;


#Test section

var managers=pm.environment.get("managers");
if(managers && managers.length>0){
    postman.setEnvironmentVariable("currentmanager",managers.shift());
    postman.setNextRequest("https://example.com");
}
else{
    postman.clearEnvironmentVariable("manager");
     postman.clearEnvironmentVariable("managers");
