#Semaphore几个常见初始值及含义


wait(); //--，如果进入了之后就会block

signal();//++， 可能释放被wait的

 
sem = 5； → 5个可以入场

sem = 1； → mutex，就是只许一个入场

>In computer programming, a mutex is a program object that allows multiple program threads to share the same resource, such as file access, but not simultaneously. When a program is started, a mutex is created with a unique name

sem = 0; // first process to call wait()


```
p1 
}
wait()
}

p2 
}
signal();
}

```

P1 waits for p2



acquire(): Acquires a permit, if one is available and returns immediately, reducing the number of available permits by one.



release():Releases a permit, increasing the number of available permits by one，也就是signal
