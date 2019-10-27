### ```First Program```
```fortran
program first_program
    
    implicit none ! treats all variables that start with the letters i, j, k, l, m and n as integers and all other variables as real arguments
    character* 20::name
    character (len=20)::f_name,l_name
    
    print*, "What's your name? "
    read*, f_name,l_name
    print*, "Hello ",trim(f_name)," ",trim(l_name)  ! trim(x): removes any white spaces left
    
    
end program first_program
```



