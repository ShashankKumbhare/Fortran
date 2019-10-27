## Welcome to Learning Fortran 

#### Content
  
[1. First Program](#1-First-Program)  
[2. Variable Types](#2-Variable-Types)  
[3. Print formatting](#3-Print-formatting)  
[4. Math Operators](#4-Math-Operators)  
[5. Math Functions](#5-Math-Functions)  
[6. Conditionals](#6-Conditionals)  
[7. Looping](#7-Looping)  
[8. Arrays](#8-Arrays)  
[9. Multidimentional Arrays](#8-Multidimentional-Arrays)  
[](#)
[](#)
[](#)
[](#)
[](#)
[](#)
[](#)  




### <p align="center">```1-First Program```</p>  
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
```
 What's your name?
Shashank Kumbhare
 Hello Shashank Kumbhare
```

### <p align="center">```2-Variable Types```</p>  
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
```
 Biggest Real  3.4028235E+38
 Biggest Int  2147483647
 Smallest Real  1.1754944E-38
 Int            4
 Real            4
 Double            8
 Logical            4
 Character            1
October   0
```

### <p align="center">```3-Print formatting```</p>  
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
```
 A number           10          15         100

    7    6    8

    7
    6
    8

    7
    6
    8

  7  6
  8

           7           6           8

 3.14150 1.12340

    Name     Age

0.1234E+020.1235E+03

I am 43

A number 10
```

### <p align="center">```4-Math Operators```</p>  
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
```
   5+4= 9
   5-4= 1
   5*4= 20
   5%4= 1
  5**4= 625
2.222222328186035
2.222222222222222
 1
```

### <p align="center">```5-Math Functions```</p>  
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
```
ABS(-1) = 1
SQRT(81) = 9.0
EXP(1) = 2.71828
LOG(2.71) = 0.99695
INT(2.71) = 2
NINT(2.71) = 3
FLOOR(2.71) = 2
MAX(2.7,3.4) = 3.4
MIN(2.7,3.4) = 2.7
SIN(1.5708) = 1.0
COS(1.5708) = -.000
TAN(1.5708) = -276243.84375
ASIN(0) = 0.000
ACOS(0) = 1.571
ATAN(0) = 0.000
```

### <p align="center">```6-Conditionals```</p>  
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
```
 Middle School
 T
 F
 T
 T
 Middle School
```

### <p align="center">```7-Looping```</p>  
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
end program $7looping
```
```
1
3
5
7
9

2
4
6
8

 What's your guess
5
 What's your guess
1
 What's your guess
9
 What's your guess
7
```

### <p align="center">```8-Arrays```</p>  
```fortran
program $8arrays
    implicit none
    
    integer :: n
    ! Create ARRAY
    integer, dimension(1:5) :: a1, a2, a3
 
    ! Assign values (Starts at index 1)
    a1(1) = 5
    ! Retrieve value
    print"(i1,/)", a1(1)
    
    ! Assign values with a loop
    do n=1,5
        a1(n)=n
        print"(i1)", a1(n)
    end do    
    
    ! Get size
    print"(/,i2)", size(a1) 
    
    ! Get a range
    print"(/,3i2)", a1(1:3)
    
    ! Get a range with an increment
    print"(/,2i2)", a1(1:3:2)
    
end program $8arrays
```
```
5

1
2
3
4
5

 5

 1 2 3

 1 3
```

### <p align="center">```9-Multidimentional Arrays```</p>  
```fortran
program $9multidimentional_arrays
    implicit none
    
    integer :: n, m
    ! Create multidimensional array (Matrix)
    integer, dimension(3,3) :: a4
!------------------------------------------------------------------------
    ! Assign values to a multidimensional array
    do n=1,3
        do m=1,3
            a4(n,m)=n
        end do
    end do
    do n=1,3
        do m=1,3
            print"(a2,i1,a1,i1,a4,i1)", "a(", n, ",", m, ") : ", a4(n,m)
        end do
    end do       
!------------------------------------------------------------------------  
    print*, ""
!------------------------------------------------------------------------  
    ! Use an implied do loop to print each row
    ! on one line
    do n=1,3
        print "(3i1)", (a4(n,m), m=1,3)
    end do
!------------------------------------------------------------------------
    print*, ""
!------------------------------------------------------------------------ 
    ! Get size
    print"(i2)", size(a4)
    
    ! Number of dimensions
    print "(i2)", Rank(a4)
  
    ! Elements in each dimension
    print "(i2)", shape(a4)
    
end program $9multidimentional_arrays
```
```
a(1,1) : 1
a(1,2) : 1
a(1,3) : 1
a(2,1) : 2
a(2,2) : 2
a(2,3) : 2
a(3,1) : 3
a(3,2) : 3
a(3,3) : 3

111
222
333

 9
 2
 3
 3
```

### <p align="center">```10```</p>  
```fortran

```
```

```

### <p align="center">```11```</p>  
```fortran

```
```

```

### <p align="center">```12```</p>  
```fortran

```
```

```

### <p align="center">```13```</p>  
```fortran

```
```

```

### <p align="center">```14```</p>  
```fortran

```
```

```

### <p align="center">```15```</p>  
```fortran

```
```

```

### <p align="center">```15```</p>  
```fortran

```
```

```

### <p align="center">```16```</p>  
```fortran

```
```

```

### <p align="center">```17```</p>  
```fortran

```
```

```

### <p align="center">```18```</p>  
```fortran

```
```

```


