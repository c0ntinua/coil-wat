![Screenshot 2023-01-19 at 6 58 54 AM](https://user-images.githubusercontent.com/90075803/213439000-0bf02af5-1bff-4e45-add5-3385ac2b3bb7.png)
# coil-wat
cellular automata rules applies to themselves as seed (evolving)

This Web Assembly program, written by hand in the text format and not compiled from some other source code, implements and displays a special kind of elementary cellular automata with unicode full blocks. This automaton is 'special' because each row is both the current state or seed and the current rule. In other words, the current rule is mutated according to that current rule. Occasionally a fixed point is discovered within the set number of rows (32), which is bound to happen anyway after enough time steps (within 2^32). 


