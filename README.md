
# Mastering Hibernate
 * When working on projects i felt that i'm able to map the entities but i was not aware
   of the some concepts like what is the purpose of using @JoinColumn annotation, why we use mappedBy attribute and many more.
   So in this repository i'm going to clear all these concepts by defining in simple english.

   I have gathered all this material from several resources like YouTube, Baeldung etc.

   This is only for my learning purpose, In case if you liked my work then you can star this repository as an appreciation. 


### @JoinColumn()

The @JoinColumn annotation defines the actual physical mapping on the owning side.
In simple words @JoinColumn annotation requires a name attribute which should come from the database table.

eg.
```java
@Entity
class Student{
    @Id
    @Column(name="student_id")
    private int id;
    private String name;
    @OneToOne
    @JoinColumn(name="address_id")
    private Address address;
}

class Address{
    @Id
    @Column(name="address_id")
    private int id;
    private Student student;
}
```
The reason of adding @JoinColumn annotation is that in the database we dont want to see any complicated name. So, we are giving our own simple name for that particular foreign key.
Before adding @JoinColumn annotation the name would look like this **address.address_id** which is not good.
after adding annotation the name would be simpler like **address_id**;


### mappedBy (it's an attribute)
 The referencing side is defined using the mappedBy attribute of the @OneToMany annotation.
 It is used in bidirectional mapping where we specify the column (instance variable name) on which we want to map.
 
 eg.
```java
@Entity
class Student{
    @Id
    @Column(name="student_id")
    private int id;
    private String name;
    @OneToOne
    @JoinColumn(name="address_id")
    private Address address;
}

class Address{
    @Id
    @Column(name="address_id")
    private int id;
    @OneToOne(mappedBy="address") // address is the instance variable of student class.
    private Student student;
}
```
