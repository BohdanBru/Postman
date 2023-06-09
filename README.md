
__Postman study project__

_In this project, I used swapi.dev/api, where I was did:_
* request to server 
* automation test:
  * Create schema: "If body properties are correct"
  * Create schema: "If body's type properties are correct"
   * 1. correct response format JSON
   * 2. We have all the declared fields in the response
   * 3. Field value in not null
   * 4. Check if value isn't empty
   * 5. Check if field correcponds to a specific value
   * 6. Status code is 200
   * 7. Status massage is ok
   * 8. Response time is less then 1000 ms
   * 9.There is the specific header in the response
   * 10. The response has a spacific header with a spacific value
   * 11. Coockie exist
   * 12. Coockie has value


__Example__

1. correct response format JSON
~~~json
pm.test("Correct response JSON format", function(){
    pm.response.to.have.jsonBody()
});
~~~
        
2. We have all the declared fields in the response
~~~json
pm.test("Check that we have all declared fiels", function(){
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("people");
    pm.expect(jsonData).to.have.property("planets");
    pm.expect(jsonData).to.have.property("films");
    pm.expect(jsonData).to.have.property("species");
    pm.expect(jsonData).to.have.property("vehicles");
    pm.expect(jsonData).to.have.property("starships");
});
~~~
        
3. Field value in not null
~~~json
pm.test("Check if value isn't null", function(){
    var jsonData = pm.response.json();
    pm.expect(jsonData.people).not.equal(null);
    pm.expect(jsonData.planets).not.equal(null);
    pm.expect(jsonData.films).not.equal(null);
    pm.expect(jsonData.species).not.equal(null);
    pm.expect(jsonData.ehicles).not.equal(null);
    pm.expect(jsonData.starships).not.equal(null);

});
~~~
        
4. Check if value isn't empty
~~~json
pm.test("Check if value is empty", function(){
    var jsonData = pm.response.json();
    pm.expect(jsonData.people).not.equal("");
    pm.expect(jsonData.planets).not.equal("");
    pm.expect(jsonData.films).not.equal("");
    pm.expect(jsonData.species).not.equal("");
    pm.expect(jsonData.ehicles).not.equal("");
    pm.expect(jsonData.starships).not.equal("");

});
~~~
            
5. Check if field correcponds to a specific value
~~~json        
pm.test("Check if field correcponds to a specific value", function(){
    var jsonData = pm.response.json();
    pm.expect(jsonData.people).to.equal("https://swapi.dev/api/people/");
    pm.expect(jsonData.planets).to.equal("https://swapi.dev/api/planets/");
    pm.expect(jsonData.films).to.equal("https://swapi.dev/api/films/");
    pm.expect(jsonData.species).to.equal("https://swapi.dev/api/species/");
    pm.expect(jsonData.vehicles).to.equal("https://swapi.dev/api/vehicles/");
    pm.expect(jsonData.starships).to.equal("https://swapi.dev/api/starships/");
});
 ~~~       
6. Status code is 200
 ~~~json      
pm.test("Status code is 200", function(){
    pm.response.to.have.status(200);
})
~~~
7. Status massage is ok
 ~~~json       
pm.test("Status massage is ok", function(){
    pm.response.to.have.status("OK");
});
~~~      
8. Response time is less then 1000 ms
~~~json        
pm.test("Response time is less then 1000 ms", function(){
    pm.expect(pm.response.responseTime).to.be.below(1000);
});
~~~      
9.There is the specific header in the response
 ~~~json       
pm.test("There is the specific header in the response", function(){
    pm.response.to.have.header("Content-Type");
});
 ~~~       
10. The response has a spacific header with a spacific value
~~~json
pm.test("The response has a spacific header with a spacific value", function(){
    pm.response.to.be.header("Content-Type", "application/json");
});
 ~~~
11. Coockie exist
~~~json
pm.test("Coockie exist", function(){
    pm.cookies.has("__cfduid")
});
 ~~~       
12. Coockie has value
 ~~~json       
pm.test("Coockie has value", function(){
    try{
        var MY_COOCKIE = pm.cookies.get("__cfduid");
        console.log(MY_COOCKIE);
    }catch(e){
        console.log("SOME PROBLEM WITH COOCKIE -> " + e);

    }
});  
~~~

Build schema for check if body in response properties and types are corect
~~~json 
var data = JSON.parse(responseBody);
var schema = {
    //specifi the type of object
    "type": "object",
    //specify requiret properties
    "requiret" : ["people", "planets", "films", "species", "vehicles", "starships"],
    //discribe the properties
    "properties" : {
        "people": {"type": "string"},
        "planets": {"type": "string"},
        "films": {"type": "string"},
        "species": {"type": "string"},
        "vehicles": {"type": "string"},
        "starships": {"type": "string"},
    }
};
pm.test("Body is correct", function(){
    pm.expect(tv4.validate(data, schema)).to.be.true;
});
~~~
https://swapi.dev/api/people/1
~~~json
var data = JSON.parse(responseBody);
var schema = {
    "type" :  "object",
    "requared" : ["name", "homeworld", "films", "species", "vehicles", "starships"],
    "properties" :{
        "name" : {"type": "string"},
        "homeworld": {"type": "string"},
        "films" : {
            "type": "array",
            "items" : {"type": "string"}
        },
        "species" : {
            "type" : "array",
            "items" : {"type": "string"}
        },
        "vehicles": {
            "type" : "array",
            "items" : {"type": "string"}
        },
        "starships": {
            "type" : "array",
            "items" : {"type": "string"}
        },
    }
};
pm.test("Body is correct", function(){
    pm.expect(tv4.validate(data, schema)).to.be.true;
});
~~~

