# Entity Framework

Why EF is considered as slow
By default EF has lazy loading behavior. Due to this default behavior if you are loading a large number of records and especially if they have foreign key relationships, you can have performance issues. So you need to be cautious if you really need lazy loading behavior for all scenarios. For better performance, disable lazy loading when you are loading a large number of records or use stored procedures.
Lazy loading
Lazy loading is the process whereby an entity or collection of entities is automatically loaded from the database the first time that a property referring to the entity/entities is accessed
Pour avoir du lazy loading il faut que la méthode soit virtuelle ! Si pas virtuelle  eager loading
Disable lazy loading : context.ContextOptions.LazyLoadingEnabled = false; + Include à chaque fois
Eager loading
Include in your query ou context.Entry(post).Reference(p => p.Blog).Load(); 

Lazy loading et serialization
Attention car Serialization fait souvent appel à tous les champs  load  ca va prendre du temps alors que ce n’est peut-être pas nécessaire
Eagerly loading multiple levels
Include(s => s.Subs.Select(x => x.SubSubs)
What’s the difference between LINQ to SQL and Entity Framework?
•	LINQ to SQL is good for rapid development with SQL Server. EF is for enterprise scenarios and works with SQL Server as well as other databases.
•	LINQ maps directly to tables. One LINQ entity class maps to one table. EF has a conceptual model and that conceptual model maps to the storage model via mappings. So one EF class can map to multiple tables, or one table can map to multiple classes.
•	LINQ is more targeted towards rapid development while EF is for enterprise level where the need is to develop a loosely coupled framework.
Collections or List ?
Here's the difference between the interfaces:
•	IEnumerable<T> is read-only
•	You can add and remove items to an ICollection<T>
•	You can do random access (by index) to a List<T>
	ICollection is the more appropriate but List<T> works also as EF will create List at the end
How to ignore a field in an entity
NotMappedAttribute
How to handle transactions in Entity Framework ?
The “SaveChanges()” method in Entity Framework operates within a transaction and saves results of the work.
using (var transaction = context.Database.BeginTransaction())
How to disable entity validation when onSaveChanges is called ?
Context.Configuration.ValidateOnSaveEnabled = false;

Custom conventions
DbContext.OnModelCreating
modelBuilder.Properties<int>()
                .Where(p => p.Name == "Key")
                .Configure(p => p.IsKey());
Ou
modelBuilder.Properties()
                .Where(x => x.GetCustomAttributes(false).OfType<NonUnicode>().Any())
                .Configure(c => c.IsUnicode(false));

public class DateTime2Convention : Convention
    {
        public DateTime2Convention()
        {
            this.Properties<DateTime>()
                .Configure(c => c.HasColumnType("datetime2"));        
        }
    }
+ modelBuilder.Conventions.Add(new DateTime2Convention());

Inheritance strategies
If 3 classes : Mother, Daughter1 and Daughter2
•	Table per Hierarchy (TPH): This approach suggests one table for the entire class inheritance hierarchy. The table includes a discriminator column which distinguishes between inheritance classes. This is a default inheritance mapping strategy in Entity Framework. (1 table + discriminator column)
•	Table per Type (TPT): This approach suggests a separate table for each domain class. ( 3 tables)
•	Table per Concrete Class (TPC): This approach suggests one table for one concrete class, but not for the abstract class. So, if you inherit the abstract class in multiple concrete classes, then the properties of the abstract class will be part of each table of the concrete class. ( 2 tables)
TPC and TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.
TPH customization
modelBuilder.Entity<Course>()  
    .Map<Course>(m => m.Requires("Type").HasValue("Course"))  
    .Map<OnsiteCourse>(m => m.Requires("Type").HasValue("OnsiteCourse"));
	Type column name instead of Discriminitor
TPT
modelBuilder.Entity<Course>().ToTable("Course");  
modelBuilder.Entity<OnsiteCourse>().ToTable("OnsiteCourse");
TPC
Note: Note that because the tables participating in TPC inheritance hierarchy do not share a primary key there will be duplicate entity keys when inserting in tables that are mapped to subclasses if you have database generated values with the same identity seed. To solve this problem you can either specify a different initial seed value for each table or switch off identity on the primary key property. Identity is the default value for integer key properties when working with Code First.
modelBuilder.Entity<Course>() 
    .Property(c => c.CourseID) 
    .HasDatabaseGeneratedOption(DatabaseGeneratedOption.None); 
 
modelBuilder.Entity<OnsiteCourse>().Map(m => 
{ 
    m.MapInheritedProperties(); 
    m.ToTable("OnsiteCourse"); 
}); 
 
modelBuilder.Entity<OnlineCourse>().Map(m => 
{ 
    m.MapInheritedProperties(); 
    m.ToTable("OnlineCourse"); 
});
https://msdn.microsoft.com/en-us/data/jj591617#2.6
