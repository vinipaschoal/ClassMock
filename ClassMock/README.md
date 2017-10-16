# ClassMock
Test Tool for Metadata-Based and Reflection-Based Components

## 1.	Introduction
ClassMock is a framework that helps the creation of unit tests for components that use reflection or annotations. In this kind of classes, the behavior is dependent of the class structure. This way, each test case usually works with a different class created specifically for the test. With ClassMock is possible to define and generate classes in runtime, allowing a better test readability and logic sharing between tests.

## 2.	Features
The ClassMock framework has a very intuitive API that allows you to:

01. create dynamic Annotation;
02. create dynamic Enum;
03. create dynamic Interface;
04. create dynamic Abstract Class;
05. create dynamic Concrete Class;
06. Add a superclass;
07. Add interfaces;
08. Add instance fields;
09. Add static fields;
10. Set java version;
11. Set visibility (PRIVATE, PUBLIC, PROTECTED);
12. Set modifiers (VOLATILE, STATIC, FINAL, SYNCHRONIZED...);
13. Apply annotations;
14. Apply generic at superclass; 

## 3.	Install

The first step is to add the library file in your project.

#### If you use Maven:
Add in your pom.xml file
```xml
<dependency>
  <groupId>net.sf.esfinge</groupId>
  <artifactId>classmock</artifactId>
  <version>2.0</version>
</dependency>
```
#### If you prefer download of file:
The library can be downloaded in [ClassMock](https://oss.sonatype.org/content/groups/staging/net/sf/esfinge/classmock/2.0/).

## 4. Tutorial:

### 4.1 Five seconds tutorial:

Bellow is a simple example of use.

```java
// Without package
Class<?> yourClass = ClassMock.of("YoursUniqueDynamicClassName").build();

//or with a declared package
Class<?> yourClass = ClassMock.of("my.pack.org.fake.domain.YoursUniqueDynamicClassName").build();
```

### 4.2 Ten seconds tutorial:

Creating a class or interface.

```java
// Create a Concrete Class
final Class<?> clazz = ClassMock.of("MyEspecialClass").build();

// Create an Abstract Class
final Class<?> absClazz = ClassMock.of("AbstractMyEspecialClass").asAbstract.build();

// Create an Interface
final Class<?> interf = ClassMock.of("IMyEspecialClass").asInterface.build();

// Create an Annotaion
final Class<?> annotation = ClassMock.of("MyEspecialAnnotationClass").asAnnotation.build();

// Create an Enum
final Class<?> annotation = ClassMock.of("MyEspecialAnnotationClass").asAnnotation.build();
```

### 4.1 One minute tutorial:

A simple example of JPA entity.

```java
final IClassWriter mock = ClassMock.of("SingleClassName");
mock.superclass(MySuperClass.class);
mock.interfaces(Serializable.class);
mock.annotation(Entity.class)
                        .and()
                        .annotation(Table.class)
                        .property("schema", schemaName)
                        .property("name", tableName);
mock.field("serialVersionUID", long.class)
                        .modifiers(ModifierEnum.STATIC, ModifierEnum.FINAL)
                        .value(4376923548604344061L)
                        .visibility(VisibilityEnum.PRIVATE);
mock.field("id", Integer.class)
                        .annotation(Id.class)
                        .and()
                        .annotation(Column.class)
                        .property("name", "ID_CODE");
mock.field("name", String.class)
                        .annotation(Column.class)
                        .property("name", "TX_NAME");
mock.field("age", Integer.class)
                        .annotation(Column.class)
                        .property("name", "NU_AGE")
                        .property("nullable", false);
mock.field("total", Float.class)
                        .annotation(Transient.class)
                        .hasGetter(true)
                        .hasSetter(false);

Class<?> jpaClazz = ClassMock.of("MyEspecialClass").build();
Object instance = clazz.newInstance();
```

### 4.2 Enum tutorial:

A simple example of Enum.

```java
final IClassWriter mock = ClassMock.of(this.getClassName()).asEnum();

Arrays.asList("BMW", "BENTLEY", "PORSCHE", "CADILLAC", "LEXUS", "FERRARI", "MERCEDES", "FORD")
            .forEach(car -> {

                mock.field(car, Enum.class)
                                .hasGetter(false)
                                .hasSetter(false)
                                .visibility(VisibilityEnum.PUBLIC)
                                .modifiers(ModifierEnum.FINAL, ModifierEnum.STATIC, ModifierEnum.ENUM);
            });

final Class<?> clazz = mock.build();
final Object[] enumConstants = clazz.getEnumConstants();
```

### 4.3 Annotation tutorial:

A simple example of Annotation.

```java
final IClassWriter mock = ClassMock.of(this.getClassName()).asAnnotation();
mock.method("alias")
                .returnType(String.class)
                .visibility(VisibilityEnum.PUBLIC)
                .modifiers(ModifierEnum.ABSTRACT);
mock.method("query")
                .returnType(String.class)
                .visibility(VisibilityEnum.PUBLIC)
                .modifiers(ModifierEnum.ABSTRACT);
mock.method("active")
                .returnType(Boolean.class)
                .visibility(VisibilityEnum.PUBLIC)
                .modifiers(ModifierEnum.ABSTRACT)
                .value(Boolean.TRUE); // default value for this property

final Class<?> annotation = mock.build();
```

### 4.4 More tutorials:

See our tests section in the project.

### [MIT Licensed](LICENSE)