![Screenshot 2023-01-19 at 6 58 54 AM](https://user-images.githubusercontent.com/90075803/213439000-0bf02af5-1bff-4e45-add5-3385ac2b3bb7.png)
# coil-wat


This Web Assembly program, written by hand in the text format and not compiled from some other source code, implements and displays a special kind of elementary cellular automata with unicode full blocks. This automaton is 'special' because each row is both the current state or seed and the current rule. In other words, the current rule is mutated according to that current rule. Occasionally a fixed point is discovered within the set number of rows (32), which is bound to happen anyway after enough time steps (within 2^32). I basically ported Rust code (also in this repo) which uses the rotation of bits extensively. 

The more complicated/essential part of the program is:



    (func $neighbor_code (param $x i32) ( param $i i32) (result i32)
        (i32.rotr ( i32.and ( i32.rotl (i32.const 31 ) (local.get $i)) (local.get $x) ) (local.get $i))
    )
    (func $eval (param $f i32) (param $i i32) (result i32)
        (i32.rotr (i32.and ( i32.rotl (i32.const 1) (local.get $i) ) (  local.get $f )) (local.get $i))
    )
    (func $next (param $s i32) (param $f i32) (param $i i32) (result i32)
        (i32.rotl (call $eval (local.get $f) (call $neighbor_code (local.get $s) (local.get $i))) (i32.add (local.get $i) (i32.const 3)))
    
    )
    (func $turn (param $s i32) (param $f i32) (result i32)
        (local $i i32)
        (local $r i32)
        (local.set $r (i32.const 0))
        (local.set $i (i32.const 0)) 
        (loop $loop 
            (local.set $r (i32.or (local.get $r) (call $next (local.get $s) (local.get $f)(local.get $i))))
            (local.set $i (i32.add (local.get $i) (i32.const 1)))
            (br_if $loop (i32.ge_s (i32.const 32) (local.get $i)))
            
        )
        (local.get $r)
    )
    
    
