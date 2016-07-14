# Abstract-Classes-vs.-Interfaces
The choice of whether to design your functionality as an interface or an abstract class  can sometimes be a difficult one. An abstract class is a class that cannot be instantiated, but must be inherited from. An abstract class may be fully implemented, but is more usually partially implemented or not implemented at all, thereby encapsulating common functionality for inherited classes. For details, see Abstract Classes.
An interface, by contrast, is a totally abstract set of members that can be thought of as defining a contract for conduct. The implementation of an interface is left completely to the developer.
Both interfaces and abstract classes are useful for component interaction. If a method requires an interface as an argument, then any object that implements that interface can be used in the argument. For example:
// C#
public void Spin (IWidget widget)
{}
This method could accept any object that implemented IWidget as the widget argument, even though the implementations of IWidget might be quite different. Abstract classes also allow for this kind of polymorphism, but with a few caveats:
Classes may inherit from only one base class, so if you want to use abstract classes to provide polymorphism to a group of classes, they must all inherit from that class.
Abstract classes may also provide members that have already been implemented. Therefore, you can ensure a certain amount of identical functionality with an abstract class, but cannot with an interface.
Here are some recommendations to help you to decide whether to use an interface or an abstract class to provide polymorphism for your components.
If you anticipate creating multiple versions of your component, create an abstract class. Abstract classes provide a simple and easy way to version your components. By updating the base class, all inheriting classes are automatically updated with the change. Interfaces, on the other hand, cannot be changed once created. If a new version of an interface is required, you must create a whole new interface.
If the functionality you are creating will be useful across a wide range of disparate objects, use an interface. Abstract classes should be used primarily for objects that are closely related, whereas interfaces are best suited for providing common functionality to unrelated classes.
If you are designing small, concise bits of functionality, use interfaces. If you are designing large functional units, use an abstract class.
If you want to provide common, implemented functionality among all implementations of your component, use an abstract class. Abstract classes allow you to partially implement your class, whereas interfaces contain no implementation for any members.



 
The abstract modifier indicates that the thing being modified has a missing or incomplete implementation. The abstract modifier can be used with classes, methods, properties, indexers, and events. Use the abstract modifier in a class declaration to indicate that a class is intended only to be a base class of other classes. Members marked as abstract, or included in an abstract class, must be implemented by classes that derive from the abstract class.
Example
In this example, the class Square must provide an implementation of Area because it derives from ShapesClass:
C#

abstract class ShapesClass
{
    abstract public int Area();
}
class Square : ShapesClass
{
    int side = 0;

    public Square(int n)
    {
        side = n;
    }
    // Area method is required to avoid
    // a compile-time error.
    public override int Area()
    {
        return side * side;
    }

    static void Main() 
    {
        Square sq = new Square(12);
        Console.WriteLine("Area of the square = {0}", sq.Area());
    }

    interface I
    {
        void M();
    }
    abstract class C : I
    {
        public abstract void M();
    }

}
// Output: Area of the square = 144
Abstract classes have the following features:
An abstract class cannot be instantiated.
An abstract class may contain abstract methods and accessors.
It is not possible to modify an abstract class with the sealed (C# Reference) modifier because the two modifers have opposite meanings. The sealed modifier prevents a class from being inherited and the abstract modifier requires a class to be inherited.
A non-abstract class derived from an abstract class must include actual implementations of all inherited abstract methods and accessors.
Use the abstract modifier in a method or property declaration to indicate that the method or property does not contain implementation.
Abstract methods have the following features:
An abstract method is implicitly a virtual method.
Abstract method declarations are only permitted in abstract classes.
Because an abstract method declaration provides no actual implementation, there is no method body; the method declaration simply ends with a semicolon and there are no curly braces ({ }) following the signature. For example:
public abstract void MyMethod();
The implementation is provided by an overriding methodoverride (C# Reference), which is a member of a non-abstract class.
It is an error to use the static or virtual modifiers in an abstract method declaration.
Abstract properties behave like abstract methods, except for the differences in declaration and invocation syntax.
It is an error to use the abstract modifier on a static property.
An abstract inherited property can be overridden in a derived class by including a property declaration that uses the override modifier.
For more information about abstract classes, see Abstract and Sealed Classes and Class Members (C# Programming Guide).
An abstract class must provide implementation for all interface members.
An abstract class that implements an interface might map the interface methods onto abstract methods. For example:
C#
interface I
{
    void M();
}
abstract class C : I
{
    public abstract void M();
}
Example
In this example, the class DerivedClass is derived from an abstract class BaseClass. The abstract class contains an abstract method, AbstractMethod, and two abstract properties, X and Y.
C#
abstract class BaseClass   // Abstract class
{
    protected int _x = 100;
    protected int _y = 150;
    public abstract void AbstractMethod();   // Abstract method
    public abstract int X    { get; }
    public abstract int Y    { get; }
}

class DerivedClass : BaseClass
{
    public override void AbstractMethod()
    {
        _x++;
        _y++;
    }

    public override int X   // overriding property
    {
        get
        {
            return _x + 10;
        }
    }

    public override int Y   // overriding property
    {
        get
        {
            return _y + 10;
        }
    }

    static void Main()
    {
        DerivedClass o = new DerivedClass();
        o.AbstractMethod();
        Console.WriteLine("x = {0}, y = {1}", o.X, o.Y);
    }
}
// Output: x = 111, y = 161

In the preceding example, if you attempt to instantiate the abstract class by using a statement like this:
BaseClass bc = new BaseClass();   // Error
you will get an error saying that the compiler cannot create an instance of the abstract class 'BaseClass'.

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
Interfaces and abstract classes allow you to create definitions for component interaction. Through interfaces, you can specify methods that a component must implement without actually specifying how the method is implemented. Abstract classes allow you to create definitions for behavior while providing some common implementation for inheriting classes. Both are valuable tools for implementing polymorphic behavior in your components.

_RUS_
Интерфейсы и абстрактные классы позволяют создавать определения для взаимодействия компонентов. Через интерфейсы, вы можете указать методы, которые компонент должен реализовать без фактического указания того, как реализован метод. Абстрактные классы позволяют создавать определения для поведения, обеспечивая некоторую общую реализацию для наследования классов. Оба являются ценными инструментами для реализации полиморфного поведения в ваших компонентов.
