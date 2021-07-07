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
