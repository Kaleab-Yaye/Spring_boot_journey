# the .equals();
like the to string methode every object in java inherites this calss from the paartn calss Objec but what do we use it for.
in java when you use the == to compare object you are actually compring the mmemory reffernce to the hiip of those objects. meaning for it to retrun to true the two reffercese should be exacctrly the same

so this is not always usfull in object comparsion there could be two object occping differt loacaion in the memroy with fileds popoulated wit the same values so that is why we use the .equals() methode.
with out ovrriding and redfifingning this funciton it just does the ==. which is not that usfull

now this is what the methode looks like in teh object class
```Java
public boolean equals(Object ob){
retrun this == ob)
```
whch as you can see need to be ovriden 

now we ovveride it like this, for this exmaple i am going to use a reall Book class to see how it is done but before some points that will help us with the ovvriding

## the .getClass(); 
this function is used to determine the class of an objecc. In java every object is ripresented by one blueprint object. and from that blue print objec the jvm builds the object.  for exaple for the Class Book.
there is one object Book.class that is the blue print for the rest of Book of book objects. not the getClass() retrun the reffercnce to the blue print object;(we will use it so not this)

## the Objects(Object ob1, Object ob2)
thi is used to compare to object while avoidin the nul pointer exception

now dont get Object and Objects class confused the Objects class is a set of helper static methodes and tools that are men to be used by every one soe the Object.equals is a stataice object and this is what it looks like
```Java
public static boolean equals(Object a, Object b){
return a==b || (a!=null && a.equals b);// we check to make sure that a is not null and if it is not we use its .equals() methode that is ovrriden from the Object class
```

now we know the tools that we are gooing to use lets see how the ovverididng looks like

```Java
package Temp_java_Exercise;

import java.util.Objects;

public class Book {
    private int bin;
    private String name;
    private String  author;
    private String publishedDate;

    public Book(String author, String name, String publishedDate ){
        this.author = author;
        this.name = name;
        this.publishedDate = publishedDate;
    }

   
    @Override
    public boolean equals(Object object){
        if(this == object)//
            return true;

        if(object == null)
            return false;
        if (this.getClass()!=object.getClass())// cheking if the reffernce to there bluprint class is the same.
            return false;
        Book book = (Book) object;// this is safe since wee did all the chekc to make sure it is Book

        return this.bin==book.bin &&
                Objects.equals(this.author, book.author)&&
                Objects.equals(this.name,book.name)&&
                Objects.equals(this.publishedDate,book.publishedDate);
    }

}
```
now you might be askign why we used the Object.equalls this is becouse some of our fildes speciallly the string once could be null thus. string has its own .equal methode and callign this on a null woule resulr in 
runtime
```Eror
NullPointerException
```

now lets see what would happen if we extend this book class with Ebookclas and then have the same feilds and comparign them with this.

