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

// constrution class. Danger.
classA c = classA(param); // param constrution. explicit invoke.
classA c;  // no param constrution. ambiguity! 
/*
class A{
public:
  // if no param construct, which one should be invoke?
  A();
  A(int i =1);
}
*/
classA c(param);  // implicitly incoke. in stack.
classA *c = new classA(param);  // new in heap
boost::shared_ptr<classA> c = boost::make_shared<classA>(param);
// special
boost::shared_ptr<int[]> c = boost::make
```
