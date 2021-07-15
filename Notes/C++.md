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

```c++
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
classA c(param);  // implicitly incoke. in stack. right value.
classA *c = new classA(param);  // new in heap
boost::shared_ptr<classA> c = boost::make_shared<classA>(param);
// special
boost::shared_ptr<int[]> c = boost::make_shared<int[]>(size);
```
```c++
// exhaustive search sequence!
// Use recurse
typedef std::vector<std::vector<uint8_t>> vv_uint8;
typedef std::vector<std::vector<uint8_t>>::iterator vv_uint8_iter;
typedef std::vector<uint8_t> v_uint8;
typedef std::vector<uint8_t>::iterator v_uint8_iter;
vv_uint8 exhaustSeq(v_uint8 elems){
    if(elems.size()==1){
        return vv_uint8{elems};
    }
    vv_uint8 res;
    for(v_uint8_iter iter = elems.begin(); iter<elems.end(); ++iter){
        uint8_t elem = *iter;
        auto tmp = elems;
        tmp.erase(tmp.begin()+(iter-elems.begin()));
        vv_uint8 tmp_res = exhaustSeq(tmp);
        for(v_uint8 seq : tmp_res){
            seq.insert(seq.begin(),elem);
            res.push_back(seq);
        }
    }
    return res;
}
```