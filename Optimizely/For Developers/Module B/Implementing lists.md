#Devs #ModuleB 

[Blog post about lists](https://world.optimizely.com/blogs/bartosz-sekula/dates/2017/10/property-value-list)
Implementing lists of simple type.
- int
- double
- string
- DateTime

```c#
// Some individual item validators
[ItemRange(1, 10)]
[ItemStringLength(50)]
[ItemRegularExpression()]
[ListItems(5)] // Limit the number of items in the list
public virtual IList<DateTime> ListOfDates { get; set; }
```

![[Pasted image 20250604144711.png]]
