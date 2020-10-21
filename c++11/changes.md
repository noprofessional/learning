# rule of three

> If a class requires a user-defined destructor, 
> a user-defined copy constructor, 
> or a user-defined copy assignment operator, 
> it almost certainly requires all three.

So if you define any one of these three, the generation of 
copy constructer is marked as decaperated thus cause a compiler warning.

You can solve this by 
1. remove the user-defined function above if don't need it
1. explicit set funcion=default like this
    ```c
    MyClass(const MyClass&) = default;
    MyClass(MyClass&&) = default;
    MyClass& operator=(const MyClass&) = default;
    MyClass& operator=(MyClass&&) = default;
    ```
1. or define this function youself.
