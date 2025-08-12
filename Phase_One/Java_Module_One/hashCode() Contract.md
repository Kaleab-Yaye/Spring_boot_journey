# what is hash code()
now assume you hava a store of object, like million of thema dn now you want to add a new object to the list or stroe of object but you want to know wethere you are adding sn obrect
that already exists or not. the normal way woudl be to go though all the objec tiwth the for each loop and then comparign them invidually. which is even for computers hard to do
as the numebr grows exponentially. instead you would implemtn what is called thh hash set\
## how does an hash set work

imgine this when you go to the libeary the liberay is nto just a row of books in one shellf. there are many shelfg with names telling you what books you shoul expect in those shelvs
when you want to fing a book in physics you dont look at each book one by one instead you go the shelf where there it says the "physics seciton" or smtn like that now from there
your search has not come down to comparting 50 books from cmparing 20k books. the smae goes for hashed list, instea of strign object like the classic lissts they use maticmaticall
calcualtion to gether object togethere, in to backetes( this would be the shelff) so when you soeas the .containes() on the hashed list it does the caculation goes to teh buckete
where the object should be put and use the .equals() to look for th eobject or to add it that is hash in short

now the fundamental rule is if thow object are equall there hashcode shoudl be equall. also the hash code indefualt only takes count of the refernce values and not the acutall object
so if you ovveride you equala() methode you shoudl do the smae with hash code too.

every object inherite the .hashCode() from the parent Object class.

so we the Objects.hashCode() to cualucalte the hash code for our custom class 

so let looka at this code we have last time
```java
package Temp_java_Exercise;

import java.util.Objects;

public class Book {
    private int bin;
    private String name;
    private String  author;
    private String publishedDate;

    public Book(String author, String name, String publishedDate, int bin ){
        this.author = author;
        this.name = name;
        this.publishedDate = publishedDate;
        this.bin = bin;

    }


    @Override
    public boolean equals(Object object){
        if(this == object)//
            return true;

        if(object == null)
            return false;
        if (this.getClass()!=object.getClass())
            return false;
        Book book = (Book) object;// this is safe since wee did all the chekc to make sure it is Book

        return this.bin==book.bin &&
                Objects.equals(this.author, book.author)&&
                Objects.equals(this.name,book.name)&&
                Objects.equals(this.publishedDate,book.publishedDate);
    }

    public Book(){

    }

}

```
now as you can see the equals methode usses the three feilds to compare our feilds which we will use it inour overroad has code now we will overide this with
the help of th Objects.hash() whic is varargs methode ( it take on many arguments)

```package Temp_java_Exercise;

import java.util.Objects;

public class Book {
    private int bin;
    private String name;
    private String  author;
    private String publishedDate;

    public Book(String author, String name, String publishedDate, int bin ){
        this.author = author;
        this.name = name;
        this.publishedDate = publishedDate;
        this.bin = bin;

    }


    @Override
    public boolean equals(Object object){
        if(this == object)//
            return true;

        if(object == null)
            return false;
        if (this.getClass()!=object.getClass())
            return false;
        Book book = (Book) object;// this is safe since wee did all the chekc to make sure it is Book

        return this.bin==book.bin &&
                Objects.equals(this.author, book.author)&&
                Objects.equals(this.name,book.name)&&
                Objects.equals(this.publishedDate,book.publishedDate);
    }

    public Book(){

    }

    @Override
    public int hashCode(){
        return Objects.hash(bin,name,author,publishedDate);
    }

}
```
htis part of the code is doign the trick. now this an obejc tof this class will return an int hash value.

```
 @Override
    public int hashCode(){
        return Objects.hash(bin,name,author,publishedDate);
    }
```
but if want tyou can go deep adn see  the object.hash valles on Array.hash[object[] lis = new {....




