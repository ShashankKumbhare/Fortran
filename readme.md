## Welcome to Learning Fortran 

#### Content
  
[1. First Program](#1.-First-Program)  
[2. Variable Types](#2.-Variable-Types)  
[3. Print formatting](#3.-Print-formatting)  
[4. Math Operators](#4.-Math-Operators)  
[5. Math Functions](#5.-Math-Functions)  
[6. Conditionals](#6.-Conditionals)  
[7. Looping](#7.-Looping)  
[](#)  



### <p align="center">```1. Firasdsadst Program```</p>  
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

### <p align="center">```2. Variable Types```</p>  
```fortran
program variable_type
    
    implicit none
    
    real,parameter :: PI=3.1415    ! parameter: it say's that the variable is a constant
    real :: r_num1=0.0, r_num2=0.0   ! real: 6 digits of precision
    double precision :: dbl_num=1.111111111111111   ! double precision: 15 digits of precision
    integer :: i_num1=0, i_num2=0
    logical :: can_vote = .true.
    character(len=20) :: month="October"
    complex :: cplx_num=(2,4)
    
    print*, "Biggest Real", huge(r_num1)
    print*, "Biggest Int", huge(i_num1)
    print*, "Smallest Real", tiny(r_num1)
    
    ! kind(x): no. of bytes of variables
    print*, "Int ", kind(i_num1)    
    print*, "Real ", kind(r_num1)
    print*, "Double ", kind(dbl_num)
    print*, "Logical ", kind(can_vote)
    print*, "Character ", kind(month)
       ! ^ *: means default formatting
    
    print"(a10,i1)", month,i_num1
        !    ^ (a4,i1):(<a for string><no. of spaces aside>,<i for integer><no. of spaces aside>)    
    
end program variable_type
```

### <p align="center">```3. Print formatting```</p>  
```fortran
program $3print
    
    implicit none
    
    ! numbers are right justified by default
    print*, "A number ",10,15,100
   
    ! '/': for new line
    
    ! Format for integer: (RiW):  R=no. of times per line, i=integer , W=width for each value    
    print"(/,3i5,/)", 7,6,8
    print"(i5)", 7,6,8  ! R=1 if not provided
    print*,""
    print"(1i5)", 7,6,8
    print*,""
    print"(2i3)", 7,6,8 ! two no. on one line and rest will be on new lines each
    print"(/,3i)", 7,6,8  ! R=12 if not provided    
    
    ! Format for float: (RfW.D):  R=no. of times per line, f=float, W=width for each value, D=no. of decimal places
    print"(/,2f8.5)", 3.1415,1.1234
    
    ! Format for characters: (RaW):  R=no. of times per line, a=character, W=width for each value
    print"(/,2a8)", "Name","Age"
    
    ! Format for exponential: (ReW):  R=no. of times per line, e=exponential, W=width for each value, D=no. of decimal places
    print"(/,2e10.4)", 12.34, 123.456
    
    ! multiple type of variables
    print"(/,a5,i2)", "I am ",43
        
    ! adjustl("char"): left adjustment   
    print"(/,a,a)", "A number ", adjustl("10")    ! adjustl("char"): left adjustment   
      
end program $3print


```

### <p align="center">```4. Math Operators```</p>  
```fortran
program $4math_operators

    implicit none
    
    real :: float_num = 1.111111111111111
    real :: float_num2 = 1.111111111111111
    double precision :: dbl_num = 1.1111111111111111d+0
    double precision :: dbl_num2 = 1.1111111111111111d+0
    real :: rand(1)
    integer :: low = 1, high = 10
    
    print"(a8,i1)", "5+4= ",(5+4)
    print"(a8,i1)", "5-4= ",(5-4)
    print"(a8,i2)", "5*4= ",(5*4)
    print"(a8,i1)", "5%4= ",mod(5,4)    ! mod(x): Modulus
    print"(a8,i3)", "5**4= ",(5**4)     ! **: Exponentiation
    
    print"(f17.15)", float_num+float_num2
    print"(f17.15)", dbl_num+dbl_num2
    
    call random_number(rand)        ! random_number(rand): Generate random values between 0 and 1
    print"(i2)", low+floor((high-low+1)*rand)  
    
end program $4math_operators
```

### <p align="center">```5. Math Functions```</p>  
```fortran
program $5math_functions

    implicit none
    
    print "(a10,i1)", "ABS(-1) = ", ABS(-1)
    print "(a11,f3.1)", "SQRT(81) = ", SQRT(81.0)
    print "(a9,f7.5)", "EXP(1) = ", EXP(1.0)
    print "(a12,f7.5)", "LOG(2.71) = ", LOG(2.71)
    print "(a12,i1)", "INT(2.71) = ", INT(2.71)
    print "(a13,i1)", "NINT(2.71) = ", NINT(2.71)
    print "(a14,i1)", "FLOOR(2.71) = ", FLOOR(2.71)
    print "(a15,f3.1)", "MAX(2.7,3.4) = ", MAX(2.7,3.4)
    print "(a15,f3.1)", "MIN(2.7,3.4) = ", MIN(2.7,3.4)
    ! Trig functions use radians
    print "(a14,f3.1)", "SIN(1.5708) = ", SIN(1.5708)
    print "(a14,f5.3)", "COS(1.5708) = ", COS(1.5708)
    print "(a14,f13.5)", "TAN(1.5708) = ", TAN(1.5708)
    print "(a10,f5.3)", "ASIN(0) = ", ASIN(0.0)
    print "(a10,f5.3)", "ACOS(0) = ", ACOS(0.0)
    print "(a10,f5.3)", "ATAN(0) = ", ATAN(0.0)
    
end program $5math_functions
```

### <p align="center">```6. Conditionals```</p>  
```fortran
program $6conditionals

    implicit none

    ! Relational Operators : == /= > < >= <=
    ! Logical Operators : .and. .or. .not.
    
    integer :: age=13
    
    if ((age >= 5) .and. (age <= 6)) then
        print *, "Kindergarten"
    else if ((age >= 7) .and. (age <= 13)) then
        print *, "Middle School"
    else if ((age >= 14) .and. (age <= 18)) then
        print *, "High School"
    else
        print *, "Stay Home"
    end if
  
    print *, .true. .or. .false.
    print *, .not. .true.
    print *, 5 /= 9
    ! Can be used with letters
    print *, "a" < "b"
    
    ! Select
    select case (age)
    case (5)
    print *, "Kindergarten"
    case (6:13)
        print *, "Middle School"
    case (14,15,16,17,18)
        print *, "High School"
    case default
        print *, "Stay Home"
    end select
    
end program $6conditionals
```

### <p align="center">```7. Looping```</p>  
```fortran
program $7looping

    implicit none
    
    integer :: n=0, m=1
    integer :: secret_num=7

!---------------------------------------------------------------
    ! Start, Finish, Step
    do n=1,10,2
        print"(i1)",n
    end do
!---------------------------------------------------------------
    
    print*, ""

!---------------------------------------------------------------    
    ! Exit & Cycle
    ! Print only evens
    do while(m<10)
        if (mod(m,2)==0) then
            print"(i1)", m
            m=m+1
            cycle   ! Jumps back to beginning of loop
        end if
        m=m+1
    end do
!---------------------------------------------------------------    
     
    print*, ""

!---------------------------------------------------------------    
    ! Continue looping while a condition is true
    do while(n/=secret_num)
        print*, "What's your guess "
        read*, n   
    end do
!---------------------------------------------------------------   
  
    
end program $7looping
```

### <p align="center">```8. ```</p>  
```fortran

```

### <p align="center">```9. ```</p>  
```fortran

```

### 1. First Program
