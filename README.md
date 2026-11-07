# melkor1_arena.c3l

C3 binding for [arena](https://github.com/Melkor-1/arena) allocator in C.

# Usage

```c3
module arena_example;

import std::io;
import std::os;
import melkor1_arena;

alias ma = module melkor1_arena;

fn int main(String[] args)
{
  ma::Arena *arena = ma::arena_new(null,10000);
  if(arena == null)
  {
    io::eprintn("Memory allocation failed!");
    os::exit(1);
  }
  defer ma::arena_destroy(arena);
  
  int *data = ma::arena_alloc(arena,int::alignment,int::size);

  if(data == null)
  {
    io::eprintn("The backing storage is full. Either add a " +++
		"new pool with arena_resize() or create a new arena.");
    os::exit(1);
  }

  *data = 10;

  io::printfn("data = %d",*data);
  
  ma::arena_reset(arena);
  
  return 0;
}
```

