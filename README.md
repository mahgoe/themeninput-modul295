# Themeninput: OR-Mapper und Entity Framework

## Inhaltsverzeichnis

1. [OR-Mapper Frameworks](#or-mapper-frameworks)  
   1.1 [Produktübersicht](#produktübersicht)  
   1.2 [Sinn und Zweck](#sinn-und-zweck)  
   1.3 [Voraussetzung](#voraussetzung)  
   1.4 [Vor-/Nachteile](#vor-nachteile)  
   1.5 [Codebeispiel](#codebeispiel)
2. [Entity Framework](#entity-framework)  
   2.1 [NuGet Pakete](#nuget-pakete)  
   2.2 [DbContext Klasse](#dbcontext-klasse)  
   2.3 [Entitätsklasse](#entitätsklasse)

---

# OR-Mapper Frameworks

## Produktübersicht

Object-Relational Mapping (ORM) Frameworks sind Softwarebibliotheken, die den Zugriff auf Daten in relationalen Datenbanken erleichtern, indem sie diese Daten in Objekte umwandeln, die in einer Programmiersprache verwendet werden können.

Einige bekannte OR-Mapper Frameworks sind:

- Hibernate (Java)
- Entity Framework (C#.NET)
- Django ORM (Python)
- Sequelize (JavaScript/Node.js)
- ActiveRecord (Ruby on Rails)

## Sinn und Zweck

ORM-Frameworks ermöglichen es Entwicklern, Datenbanktransaktionen auf einer höheren, objektorienterten Ebene zu behandeln,
anstatt SQL-Abfragen direkt zu schreiben. Dies kann die Entwicklung beschleunigen und den Code lesbarer und wartbarer machen.

## Voraussetzung

Die Nutzung eines OR-Mapper erfordert:

- Kenntnisse in der jeweiligen Programmiersprache des Frameworks.
- Ein Verständnis der Datenbankstruktur.
- Eventuell spezifische Kenntnisse der gewählten ORM-Framework.
- Allfällige Konfigurationskenntnisse, weil der ORM-Frameworks oft komplex sein können.
- Verständnis von Datenbank-Transaktionen.
- Wissen, wie man ORM Testdaten erstellt und Unit-Tests durchführt.

## Vor-/Nachteile

### Vorteile:

- Beschleunigt die Entwicklung durch Abstraktion von SQL-Code.
- Fördert die Wiederverwendung von Code.
- Bietet oft zusätzliche Sicherheitsmechanismen, z. B. gegen SQL-Injection.

### Nachteile:

- Kann in manchen Fällen zu Leistungseinbussen führen.
- Nicht immer sind alle speziellen Datenbankfeatures nutzbar.
- Kann die Komplexität erhöhen, besonders bei Fehlersuche.

## Codebeispiel

### Hibernate (Java):

```java
@Entity
public class User {
    @Id
    @GeneratedValue
    private Long id;
    private String name;

    // Getter und Setter für 'id'
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    // Getter und Setter für 'name'
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

Session session = sessionFactory.openSession();
User user = new User();
user.setName("Max");
session.save(user);
```

### Entity Framework(C#.NET):

```csharp
public class User {
    public int Id { get; set; }
    public string Name { get; set; }
}

using (var context = new DbContext()) {
    User user = new User { Name = "Max" };
    context.Users.Add(user);
    context.SaveChanges();
}
```

# Entity Framework

## NuGet Pakete

Entity Framework kann über NuGet-Pakete in ein .NET-Projekt integriert werden.  
Typische Pakete sind:

- `Microsoft.EntityFrameworkCore`: Kernpaket von EF Core
- `Microsoft.EntityFrameworkCore.SqlServer`: Unterstützung für SQL Server
- `Microsoft.EntityFrameworkCore.InMemory`: Hauptsächlich für Tests

Je nach Datenbank und weiteren Anforderungen können noch andere NuGet-Pakete erforderlich sein.

## DbContext Klasse

`DbContext` ist eine zentrale Klasse in EF und dient als Haupteinstiegspunkt für jede Interaktion mit der Datenbank.  
Es repräsentiert eine Session mit der Datenbank und kann zum Abfragen und Speichern von Instanzen Ihrer Entitäten verwendet werden.

```csharp
public class MyDbContext : DbContext
{
    public DbSet<User> Users { get; set; }
}
```

## Entitätsklasse

`DbSet<TEntity>` repräsentiert eine Sammlung aller Entitäten in der Datenbank (oder in einem Tabelle/View), von einem gegebenen Typ.  
Es bietet Methoden zum Abfragen, Hinzufügen, Entfernen und Aktualisieren von Entitäten.

```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```
