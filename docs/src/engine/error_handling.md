# Error Handling

Steel provides the `stop!` macro to send errors to the Steel engine from Rust.

Errors types are defined by the enum `steel::rerrs::ErrorKind`.

```rust
use steel::stop;
use steel::rvals::Result;

use steel::steel_vm::engine::Engine;
use steel::steel_vm::register_fn::RegisterFn;

fn check_str(val: String) -> Result<String>{
    if val == "bad" {
        stop!(Generic => "This string doesn't check out!")
    }
    Ok(val)
}


pub fn main() {
    let mut vm = Engine::new();
    vm.register_fn("check_str", check_str);
    steel_repl::run_repl(vm).unwrap();
}

```

This way, when the Steel repl is run, the user can trigger errors without causing the
program to panic.

