so we have see how too install the lombok in to otu idea and we have builg its dependancy in loombok

nowe what we will do now is we run our the apiApplication and we will try to requist to our local serve to write our first hello world in the spting boot world

# the @RestContolor anotation

this anotation come emditaly before a class and this tell spting boot that this class will be used to handle the HTTP requists the PUT,Get,Post, and delete. so that the spring boot know and have few class to look
for for handling specific requists
 ## the @GetMaping anotation this anotation is written right above the methode that we wotn to reipond to the get requist and youcan have many @GetMaping methodes so you should spcify what requist they shoudl look for
 fore emxpale @GetMaping("/api/helth")
 now the methode that is very next to this anotation will give a riponce to any https requist that is get and has url that is like that.

 ## the riponce enityt 
RisponsEntitiy(T) now you can have yout getmapign methode to return an object of your need and it will turn that objec to jason format but. when you rerturn a riponce enitty
you can specifya 
* the requist state ( is it OK, 404, 400) you can do this with
  ```java
  return RisponceEntity.Ok(body) so the body is the object and you can state the name. 

  ```

  now look at this code that will handle the requist that we need
```java
  package com.bookmarked.api;

import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Map;

// we have to tell sprign boot that this class will be one of the many restContorolor class taht we will hava
@RestController
public class HelthChecker {

    @GetMapping
    public ResponseEntity<Map<String,String>> helthChecker(){
        Map<String, String> map = Map.of("Status","Working");
        return ResponseEntity.ok(map);
    }
}
```
  
