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
[9. Multidimentional Arrays](#9-Multidimentional-Arrays)  
[10. Runtime Arrays](#10-Runtime-Arrays)  
[11. Format](#11-Format)  
[12. Strings](#12-Strings)  
[13. Structures](#13-Structures)  
[14. Functions](#14-Functions)  
[15. Recursive Functions](#15-Recursive-Functions)  
[16. Subroutines](#16-Subroutines)  
[16. Subroutines](#16-Subroutines)  
[17. Modules](#17-Modules)  
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

### <p align="center">```10-Runtime Arrays```</p>  
```fortran
program $10runtime_arrays
    implicit none
    
    integer :: n, m, x, y
    integer, dimension(1:5) :: a1,a2
    integer, dimension(1:9) :: a6=(/1,2,3,4,5,6,7,8,9/)
    integer, dimension(1:3,1:3) :: a7
    ! Define an array thats size is determined at run time
    integer, dimension(:), allocatable :: a5
    integer :: num_vals = 0    
!-------------------------------------------------------------    
    ! Define array size at run time
    print*, "Enter size of array: "
    read*, num_vals
    allocate(a5(1:num_vals))
    do n=1,num_vals
        a5(n)=n
    end do   
    print"(a4,50i2)","a5= ", (a5(n), n=1,num_vals)
!-------------------------------------------------------------        
    ! Change all values in array
    a1=(/1,2,3,6,7/)
    a2=(/0,2,4,6,8/)
    print"(a4,5i2,/,a4,5i2)","a1= ", (a1(m), m=1,5), "a2= ", (a2(m), m=1,5) 
!-------------------------------------------------------------        
    ! Reshape the ARRAY from 1x9 t0 3x3
    a7 = reshape(a6,(/3,3/))
    print*, "a7="
    do n=1,3
        print"(3i2)", (a7(n,m), m=1,3)
    end do
!-------------------------------------------------------------        
    ! Check if values are equal across
    ! the 1 dimension
    print "(l1)", all(a1==a2, 1)
    ! Are any equal?
    print "(l1)", any(a1==a2, 1)
    ! How many are equal
    print "(i1)", count(a1==a2, 1)
    ! Get min and max value
    print "(i1)", maxval(a1)
    print "(i1)", minval(a1)
    ! Get product and sum
    print "(i3)", product(a1)
    print "(i2)", sum(a1)   
    
end program $10runtime_arrays
```
```
 Enter size of array:
8
a5=  1 2 3 4 5 6 7 8
a1=  1 2 3 6 7
a2=  0 2 4 6 8
 a7=
 1 4 7
 2 5 8
 3 6 9
F
T
2
7
1
252
19
```

### <p align="center">```11-Format```</p>  
```fortran
program $11format
    implicit none
    
    integer :: num
    integer :: cups
    real :: liters
    real :: quarts
    
    ! Print values (1 to 12) * 7
    do num = 1,12
        print 100, num,num*7
        ! The format statement has a numbered label. You pass values to it that will fit into the designated formatting
        ! I designates an integer along with total space with values right justified
        100 format(i2,' * 7 = ',i3)
    end do
    print "(/a18)", "Cups Liters Quarts"
    do cups = 1, 10
        liters=cups*0.236
        quarts=cups*0.208
        print 200, cups,liters,quarts
        ! x defines spaces f is for floats
        200 format(' ',i3, 2x, f5.3, 2x, f5.3)
    end do
end program $11format
```
```
 1 * 7 =   7
 2 * 7 =  14
 3 * 7 =  21
 4 * 7 =  28
 5 * 7 =  35
 6 * 7 =  42
 7 * 7 =  49
 8 * 7 =  56
 9 * 7 =  63
10 * 7 =  70
11 * 7 =  77
12 * 7 =  84

Cups Liters Quarts
   1  0.236  0.208
   2  0.472  0.416
   3  0.708  0.624
   4  0.944  0.832
   5  1.180  1.040
   6  1.416  1.248
   7  1.652  1.456
   8  1.888  1.664
   9  2.124  1.872
  10  2.360  2.080
```

### <p align="center">```12-Strings```</p>  
```fortran
program $12strings
    implicit none
    
    ! Strings are character arrays
    character (len=30) :: str="I'm a string"
    character (len=30) :: str2=" that is longer"
    character (len=30) :: str3
  
    ! Join strings that have been trimmed of whitespace
    ! You can also trim right (adjustr) and left (adjustl)
    str3 = trim(str)//trim(str2)
    print*, str3
    ! Get a substring
    print*, str3(1:3)
    ! Find the index of a substring
    print"(a9,i1)", "Index at ", index(str, "string")
    ! Get size
    print"(i2)", len(str3)
    
end program $12strings
```
```
 I'm a string that is longer
 I'm
Index at 7
30
```

### <p align="center">```13-Structures```</p>  
```fortran
program $13structures
    implicit none
    
    ! You can define custom types which contain multiple values of different types
    type Customer
        character (len = 40) :: name
        integer :: age
        real :: balance
    end type Customer
  
    type(Customer), dimension(5) :: customers  
    integer :: n
    ! Create a customer
    type(Customer) :: cust1
  
    ! Assign values
    cust1%name="Sally Smith"
    cust1%age=34
    cust1%balance=320.45
    ! Assign structure to array
    customers(1) = cust1  
    ! Assign values independently
    customers(2)%name = "Tom May"
    customers(2)%age = 42
    customers(2)%balance = 229.78
  
    do n = 1, 2
        print"(a12,i3,f8.3)", customers(n)
    end do   
end program $13structures
```
```
Sally Smith  34 320.450
Tom May      42 229.780
```

### <p align="center">```14-Functions```</p>  
```fortran
program $14functions
    implicit none
    
    integer :: ans
    
    ans=get_sum(9,4)
    print"(a8,i2)", "9 + 4 = ", ans
    print"(a8,i2)", "9 - 4 = ", get_diff(9,4)
    print"(a8,i2)", "9 + 0 = ", get_sum2(9)
    print"(a8,i2)", "9 + 4 = ", get_sum2(9,4)
    
!-----------------------------------------------------------------------------------------------------            
    ! Defines area for functions
    contains
!-----------------------------------------------------------------------------------------------------     	
        ! function, name, arguments
        function get_sum(n1,n2) result(sum)
            implicit none
            integer :: n1, n2, sum
            sum=n1+n2       ! The last value defined is returned    
        end function get_sum    
!-----------------------------------------------------------------------------------------------------    
        ! intent(in): Don't allow variable values to change
        function get_diff(n1,n2) result(diff)
            implicit none  
            integer, intent(in) :: n1, n2       ! intent(in): Don't allow variable values to change
            integer :: diff
            diff=n1-n2
        end function get_diff
!-----------------------------------------------------------------------------------------------------        
        ! Block functions from changing input variables with pure
        pure function get_sum2(n1,n2) result(sum)
            implicit none
            integer, intent(in) :: n1        
            integer, intent(in), optional :: n2     ! optional: Arguments don't need to have a value passed
            integer :: sum
            
            if(present(n2)) then
                sum=n1+n2
            else
                sum=n1
            end if
        end function get_sum2
!-----------------------------------------------------------------------------------------------------                
end program $14functions
```
```
9 + 4 = 13
9 - 4 =  5
9 + 0 =  9
9 + 4 = 13
```

### <p align="center">```15-Recursive Functions```</p>  
```fortran
program $15recursive_functions
    implicit none

    integer :: ans
    
    ans = factorial(4)
    print "(a15,i3)", "Factorial(4) = ", ans
    
    contains
        ! Recursive functions call themselves and must be labeled as such in Fortran
        recursive function factorial(n) result(fact)
            integer :: n, fact
            if (n==1) then
                fact=1
            else
                fact=n*factorial(n-1)
            end if
        end function
end program $15recursive_functions
```
```
Factorial(4) =  24
```

### <p align="center">```16-Subroutines```</p>  
```fortran
program $16subroutines
    implicit none
 
    integer :: i=1, p1, p2, p3
    call plus_three(i, p1, p2, p3)
    print"(i2,/,i2,/,i2)", i, p1, p2
 
    contains
        ! Subroutines can return multiple values
        subroutine plus_three(n, plus1, plus2, plus3)
            integer, intent(in) :: n
            integer, intent(out) :: plus1, plus2, plus3 ! Output
            plus1=n+1
            plus2=n+2
            plus3=n+3
        end subroutine plus_three
        
end program $16subroutines
```
```
 1
 2
 3
```

### <p align="center">```17-Modules```</p>  
- You have to make one more .f90 file for module.
- Compile them separately and run the main .f90 file.

##### ```.f90 file for main code```
```fortran
program $17modules
    use mult_mod    ! Import module like this
    implicit none
    
    print"(a8,i3)", "4 x 5 = ", mult(4,5)
    print"(a12,f6.3)", "4.3 x 5.2 = ", mult(4.3,5.2)

end program $17modules
```
##### ```.f90 file for module```
```fortran
module mult_mod
    implicit none
    private
    public :: mult
 
    ! We can define the 2 functions we will associate with the mult function depending on the input data types
    interface mult
        procedure mult_real, mult_int
    end interface mult
 
    contains
        function mult_real(n1,n2) result(product)
            real, intent(in) :: n1, n2
            real :: product
            product=n1*n2
        end function mult_real
 
        function mult_int(n1,n2) result(product)
            integer, intent(in) :: n1, n2
            integer :: product
            product=n1*n2
        end function mult_int
    
end module mult_mod
```
```
4 x 5 =  20
4.3 x 5.2 = 22.360
```

### <p align="center">```18```</p>  
```fortran

```
```

```