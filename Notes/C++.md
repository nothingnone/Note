# global variable
```c++
# declare (Only this!)
extern int a;
# define
int a;
int a = 1;
extern int a = 1;
# above may cause redefined error.
# attention! do not define in header file. Even use #param once.
```

# Preemptible, yield
```C++
// memset(), memcpy(). cosume much and can't get too much time piece.
void memcpyPreemptible(void * dest, void * src, size_t n) {
  int d = n >> 8;
  char* dest_p = (char*)dest;
  char* src_p = (char*)src;
  if(d > 0) {
    int i = d;
    while(i < n) {
      memcpy(dest_p, src_p, d);
      i+=d;
      dest_p+=d;
      src_p+=d;
      std::this_thread::yield();
    }
    memcpy(dest_p,src_p,d+n-i);
  }else{
    memcpy(dest_p, src_p, n);
  }
}
// same as memset().
```
# class declare, define
```c++
// constrution class. Danger.
classA c = classA(param); // param constrution. explicit invoke.
classA c;  // implicitly invoke. no param constrution. ambiguity! 
/*
class A{
public:
  // if no param construct, which one should be invoke?
  A();
  A(int i =1);
}
*/
classA c(param);  // explicitly invoke. in stack.
classA *c = new classA(param);  // new in heap
boost::shared_ptr<classA> c = boost::make_shared<classA>(param);
// special
boost::shared_ptr<int[]> c = boost::make_shared<int[]>(size);
```
# vector
```cpp
# vector func
std::vector::size 	// num of elements.
std::vector::capacity 	// size of memory applied.
std::vector::clear()	// delete all elem, set size 0, but retain capacity. delte object and call destruction, won't free pointer point to.
std::vector::reserve()  // set capacity.
```
# container's elements
```cpp
// container required copy constructor and copy assign.
// if allocator provided prefered
class A{
public:
  explicit A(const A& a):x(a.x){
  }
  void operator =(const A& a){
    x = a.x;
  }

private:
  int x;
};

```
# enum declare, define
```cpp
enum State{
A,
B=3,
C	// 4
};
State(0) == A == State::A 
int i = A;	// ok
State s = 0;	// syntax error
```
